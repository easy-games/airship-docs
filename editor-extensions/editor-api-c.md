# Editor API (C#)

### <mark style="color:$warning;">AirshipType</mark>

Used to query the types in Airship

```csharp
var exampleComponentType = AirshipType.GetType("ExampleComponent");
```

|                                                                                                                       |                                                                                                  |
| --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| <mark style="color:$primary;">string</mark> Name                                                                      | The name of the type                                                                             |
| <mark style="color:$primary;">string</mark> RuntimePath                                                               | The Runtime Lua path this type is associated with                                                |
| <mark style="color:$primary;">string</mark> AssetPath                                                                 | The Editor asset path of the file that contains this type                                        |
| <mark style="color:$primary;">string</mark> UniqueId                                                                  | A unique identifier for this type                                                                |
| <mark style="color:$warning;">AirshipType</mark>\[] BaseTypes                                                         | The types this type inherits                                                                     |
| <mark style="color:$warning;">AirshipDeclarationType</mark> DeclarationType                                           | The declaration type of this type - e.g. Behaviour, Enum, ScriptableObject or SerialziableClass. |
| <mark style="color:$primary;">bool</mark> IsAssignableFrom(<mark style="color:$warning;">AirshipType</mark> baseType) | Used to check if this type is, or inherits another type                                          |

### <mark style="color:$warning;">AirshipCustomEditors</mark>

{% columns %}
{% column %}
<mark style="color:$primary;">static</mark> <mark style="color:$warning;">AirshipEditor</mark> GetEditor(<mark style="color:$warning;">AirshipComponent</mark> component)
{% endcolumn %}

{% column %}
Used to get the editor for the specified component
{% endcolumn %}
{% endcolumns %}

### <mark style="color:$warning;">AirshipEditor</mark>

Derive from this base class to create a custom inspector for an `AirshipBehaviour`

```csharp
[AirshipCustomEditor("TypeScriptClassName")]
public class ExampleComponentEditor : AirshipEditor {
    public override void OnInspectorGUI() {
        
    }
}
```

|                                                                               |                                              |
| ----------------------------------------------------------------------------- | -------------------------------------------- |
| <mark style="color:$warning;">AirshipSerializedObject</mark> serializedObject | The serialized object                        |
| <mark style="color:$warning;">AirshipScript</mark> script                     | The script the editor is for                 |
| UnityEngine.<mark style="color:$warning;">Object</mark> target                | The target object for this editor            |
| <mark style="color:$primary;">void</mark> OnInspectorGUI()                    | The IMGUI inspector lifecycle for the editor |

### <mark style="color:$warning;">AirshipEditorGUI</mark>

Contains IMGUI drawing methods for Airship

<table><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><mark style="color:$primary;">static void</mark> HorizontalLine(<mark style="color:$warning;">Color</mark> color = default, <mark style="color:$primary;">int</mark> thickness = 1, <mark style="color:$primary;">int</mark> padding = 10, <mark style="color:$primary;">int</mark> margin = 0)</td><td>Draws a horizontal line</td></tr><tr><td><mark style="color:$primary;">static bool</mark> PropertyField(<mark style="color:$warning;">AirshipSerializedProperty</mark> property)</td><td><p>Draws the given <code>AirshipSerializedProperty</code>.</p><pre class="language-csharp"><code class="lang-csharp">var exampleProperty = serializedObject.FindAirshipProperty("exampleProperty");
AirshipEditorGUI.PropertyField(exampleProperty);
</code></pre></td></tr><tr><td><mark style="color:$primary;">static  bool</mark> PropertyField(<mark style="color:$warning;">GUIContent</mark> label, <mark style="color:$warning;">AirshipSerializedProperty</mark> property)</td><td>Draws the given <code>AirshipSerializedProperty</code> with a custom label.</td></tr><tr><td><mark style="color:$primary;">static int</mark> BeginTabs(<mark style="color:$primary;">int</mark> selectedIndex, <mark style="color:$warning;">GUIContent</mark>[] tabs)</td><td><p>Will draw a tab view, must contain an <code>EndTabs</code> call at the end of the content.</p><pre class="language-csharp"><code class="lang-csharp">selectedTabIndex = AirshipEditorGUI.BeginTabs(selectedTabIndex, new [] {
    new GUIContent("Tab 1"),
    new GUIContent("Tab 2"),
});
if (selectedTabIndex == 0) {
    // render content of tab #1
} else if (selectedTabIndex == 1) {
    // render content of tab #2
}
AirshipEditorGUI.EndTabs();
</code></pre></td></tr><tr><td><mark style="color:$primary;">static void</mark> EndTabs()</td><td></td></tr><tr><td><mark style="color:$primary;">static void</mark> BeginGroup(<mark style="color:$warning;">GUIContent</mark> label)</td><td>Begin a group (will be "grouped" in a padded frame)</td></tr><tr><td><mark style="color:$primary;">static void</mark> EndGroup()</td><td>Ends the previous group scope</td></tr></tbody></table>

