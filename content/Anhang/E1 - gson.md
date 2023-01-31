---
title: E1 - Gson
---

| **Wichtig** | Die Codebeispiele in dieser Beschreibung sind natürlich angelehnt an das Projekt, aber der Code im Projekt weicht von den Beispielen ab! |
|-|-|

Ein oft genutztes Format um Daten zu speichern oder zu übertragen ist JSON (JavaScript Object Notation - 
<a href="https://de.wikipedia.org/wiki/JavaScript_Object_Notation" target="_blank">JSON auf Wikipedia (extern) {{< de >}}</a>
).

Für die Umwandlung von Java Objekten in JSON oder zurück gibt es mehrere Libraries. Die am meisten genutzt dürften Jackson und Gson sein. In diesem Kurs werden wir für diese Aufgabe auf Gson zurück greifen.
	
# Gson in ein Maven Projekt einbinden
Um Gson zu nutzen zu können, binden wir einfach in Maven folgende Abhängigkeit ein:

```XML
<!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10.1</version>
</dependency>
```
(Die Version war zum Zeitpunkt des Verfassens die aktuelle Version. Bei der angegebenen URL kann man jederzeit sehen, ob eine neue Version verfügbar ist!)

# Object -> JSON
Um ein Objekt in JSON Text zu serialisieren, reicht es aus, sich eine Instanz von Gson zu erstellen. Darauf ist die Methode toJson aufrufbar.

Beispiel:
```Java
Gson gson = new Gson();
String jsonText = gson.toJson(someInstance, SomeType.class);
```

# JSON -> Object
Um einn JSON Text in eine Instanz umzuwandeln ist der Ablauf fast gleich - es wird lediglich fromJson aufgerufen.
Beispiel:
```Java
Gson gson = new Gson();
SomeType someInstance = gson.fromJson(jsonText, SomeType.class);
```

# Abgeleitete Klassen
Ein Problem tritt auf, wenn wir nicht wissen, von welchem Typ ein JSON Objekt ist. Wenn ich z.B. in einer Klassenhirarchie ein Interface oder eine Basis Klasse habe und dann eine List von diesem Interface oder der Basisklasse zurücklesen will in eine Instanz. Gson kann nicht wissen, von welchem Typ die Daten sind, so dass wir hier ein Problem haben.

Eine mögliche Lösung für dieses Problem kann sein:
- Eine Basisklasse haben, in der auch der Typ der Klasse in einer Instanzvariable gesichert wird.
- Dann mit einem Adapter arbeiten, so daß bem Serialisieren dieser Klasse immer die volle Klasse Serialisiert wird. Dies würde es erlauben. Die Klasse über diese Basisklasse zu serialisieren.
- Beim Deserialisieren dieser Basisklasse wird erst der typ gelesen und dann dieser Typ zur Deserialisierung verwendet.

Da dies auch bei einer Liste von Elementen notwendig ist, wird dafür auch ein Adapter erzeugt. Dann kann bei einer List über eine Annotation sichergestellt werden, dass die Serialisierung / Deserialisierung korrekt erfolgen.

## Basisklasse
```Java
package org.jadv.model;

import com.google.gson.annotations.JsonAdapter;
import lombok.Getter;
import org.jadv.serialization.SavedObjectAdapter;

/**
 * An instance that can be saved through an Adapter and contains the name of the class as field.
 */
@JsonAdapter(SavedObjectAdapter.class)
public abstract class SavedObject {
    /**
     * Class name of the
     */
    @Getter
    private final String type = getClass().getName();
}
```

## JsonSerializer&lt;SavedObject&gt;
JsonSerializer&lt;SavedObject&gt; kann für alle Klassen, die von SavedObject erben, verwendet werden, um die Serialisierung durchzuführen.
```Java
    /**
     * Serializes an SavedObject to JSON. Makes sure that the serialization is using the correct class.
     * @param object Object to serialize.
     * @param interfaceType Not used.
     * @param context Serialization context.
     * @return The JsonElement that holds the serialized object.
     */
    @Override
    public JsonElement serialize(SavedObject object, Type interfaceType, JsonSerializationContext context) {
        if (object == null) return null;
        return context.serialize(object, object.getClass());
    }
```

## JsonDeserializer&lt;SavedObject&gt;
JsonDeserializer&lt;SavedObject&gt; kann für jede Unterklasse von SavedObject erwendet werden. Es wird erst der Klassenname gelesen um dann die Serialisierung für diese Klasse durchzuführen.
```Java
    /**
     * Deserializes the SavedInstance from a json.
     * @param elem Json element to deserialize
     * @param interfaceType not used.
     * @param context Deserialization context.
     * @return The restored instance with correct class.
     * @throws JsonParseException Throws an JsonParseException if deserialization is not possible.
     */
    @Override
    public SavedObject deserialize(JsonElement elem, Type interfaceType, JsonDeserializationContext context) throws JsonParseException {
        final JsonObject wrapper = (JsonObject) elem;
        final JsonElement typeName = get(wrapper, "type");
        final Type actualType = typeForName(typeName);
        return context.deserialize(elem, actualType);
    }
```

## Nutzung der Klasse
Um eine Klasse mit dem Adapter zu deserialisieren muss nur beim Deserialisieren als Zielklasse SavedObject.class angegeben werden. Der Adapter wird dann automatisch verwendet.

Zur Serialisierung muss sonst nichts weiter gemacht werden. Hier kann die korrekte Klasse angegeben werden oder auch SavedObject.class. Der Adapter sorgt dann automatisch für die korrekte Serialisierung.

## Fertige Klasse mit Hilfsmethoden
```Java
package org.jadv.serialization;

import com.google.gson.*;
import org.jadv.model.SavedObject;

import java.lang.reflect.Type;

/**
 * Gson Adapter to (de-)serialize derived types.
 */
final public class SavedObjectAdapter implements JsonSerializer<SavedObject>, JsonDeserializer<SavedObject> {
    /**
     * Serializes an SavedObject to JSON. Makes sure that the serialization is using the correct class.
     * @param object Object to serialize.
     * @param interfaceType Not used.
     * @param context Serialization context.
     * @return The JsonElement that holds the serialized object.
     */
    @Override
    public JsonElement serialize(SavedObject object, Type interfaceType, JsonSerializationContext context) {
        if (object == null) return null;
        return context.serialize(object, object.getClass());
    }

    /**
     * Deserializes the SavedInstance from a json.
     * @param elem Json element to deserialize
     * @param interfaceType not used.
     * @param context Deserialization context.
     * @return The restored instance with correct class.
     * @throws JsonParseException Throws an JsonParseException if deserialization is not possible.
     */
    @Override
    public SavedObject deserialize(JsonElement elem, Type interfaceType, JsonDeserializationContext context) throws JsonParseException {
        final JsonObject wrapper = (JsonObject) elem;
        final JsonElement typeName = get(wrapper, "type");
        final Type actualType = typeForName(typeName);
        return context.deserialize(elem, actualType);
    }

    /**
     * Gets the type for a given name.
     * @param typeElem JsonElement with classname inside.
     * @return The requested class.
     * @throws JsonParseException Thrown if the class is not available / known.
     */
    private Type typeForName(final JsonElement typeElem) throws JsonParseException {
        try {
            return Class.forName(typeElem.getAsString());
        } catch (ClassNotFoundException e) {
            throw new JsonParseException(e);
        }
    }

    /**
     * Gets an child element of an JsonObject,
     * @param wrapper Wrapper JsonObject to get the element from.
     * @param memberName Name of the element to get.
     * @return The requested JsonElement.
     * @throws JsonParseException Thrown if the requested element is not available.
     */
    private JsonElement get(final JsonObject wrapper, String memberName) throws JsonParseException {
        final JsonElement elem = wrapper.get(memberName);
        if (elem == null) throw new JsonParseException("no '" + memberName + "' member found in what was expected to be an interface wrapper");
        return elem;
    }
}
```

## Serialisierung von Listen mit Subklassen
Bei der Serialisierung von einer Liste sollte jedes Element mit seiner eigenen Klasse serialisiert und auch wieder entsprechend deserialisiert werden. Dazu kann dann ein eigenes Adapter geschrieben werden:
```Java
package org.jadv.serialization;

import com.google.gson.*;
import org.jadv.model.SavedObject;

import java.lang.reflect.Type;
import java.util.ArrayList;
import java.util.List;

/**
 * Gson Adapter to (de-)serialize derived types.
 */
final public class ListOfSavedObjectAdapter implements JsonSerializer<List<SavedObject>>, JsonDeserializer<List<SavedObject>> {
    /**
     * Serializes a list of SavedInstance to JSON.
     * @param list Object to serialize.
     * @param interfaceType Not used.
     * @param context Serialization context.
     * @return The JsonElement that holds the serialized list.
     */
    public JsonElement serialize(List<SavedObject> list, Type interfaceType, JsonSerializationContext context) {
        if (list == null) return null;
        final JsonArray array = new JsonArray();
        for (SavedObject obj : list) {
            array.add(context.serialize(obj, SavedObject.class));
        }
        return array;
    }

    /**
     * Deserializes the list of SavedInstance from a json.
     * @param elem Json element to deserialize
     * @param interfaceType not used.
     * @param context Deserialization context.
     * @return The restored list with elements with correct class.
     * @throws JsonParseException Throws an JsonParseException if deserialization is not possible.
     */
    public List<SavedObject> deserialize(JsonElement elem, Type interfaceType, JsonDeserializationContext context) throws JsonParseException {
        List<SavedObject> result = new ArrayList<>();
        final JsonArray array = (JsonArray) elem;
        for (JsonElement element : array.asList()) {
            result.add(context.deserialize(element, SavedObject.class));
        }
        return result;
    }
}
```
