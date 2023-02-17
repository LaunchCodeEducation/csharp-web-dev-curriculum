---
title: "Dictionary"
date: 2023-01-25T13:44:27-06:00
draft: false
weight: 6
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE

---

C# also provides us a structure to store data as key/value pairs. C# calls these objects dictionaries, and they are provided by the `Dictionary` class.

Considering the gradebook example, we can improve our program using a dictionary. We’ll store the students’ grades along with their names in the same data structure. The names will be the keys, and the grades will be the values.

As with the other collection structures, in C# we must specify the types of the objects we’ll be storing when we declare a variable or parameter to be a dictionary. This means specifying both key and value data types, which are allowed to be different types for a given dictionary.

You can find the `DictionaryGradebook` project in the [csharp-web-dev-examples](https://github.com/LaunchCodeEducation/csharp-web-dev-examples) repository. Explore it, run it, and notice how it differs from the `ListGradebook` and the `ArrayGradebook`. 

```csharp{linenos=table}
Dictionary<string, double> students = new Dictionary<string, double>();
string newStudent;

Console.WriteLine("Enter your students (or ENTER to finish):");

// Get student names and grades
do
{
   Console.WriteLine("Student: ");
   string input = Console.ReadLine();
   newStudent = input;

   if (!Equals(newStudent, "")) {
      Console.WriteLine("Grade: ");
      input = Console.ReadLine();
      double newGrade = double.Parse(input);
      students.Add(newStudent, newGrade);

      // Read in the newline before looping back
      Console.ReadLine();
   }

} while(!Equals(newStudent, ""));

// Print class roster
Console.WriteLine("\nClass roster:");
double sum = 0.0;

foreach (KeyValuePair<string, double> student in students) {
   Console.WriteLine(student.Key + " (" + student.Value + ")");
   sum += student.Value;
}

double avg = sum / students.Count;
Console.WriteLine("Average grade: " + avg);
```

Notice how a `Dictionary` called students is declared on line 2:

```csharp{linenos=table,hl_lines=[],linenostart=2}
Dictionary<string, double> students = new Dictionary<string, double>();
```

Here, `<string, double>` defines the data types for this dictionary’s` <key, value>` pairs.

We can add a new item with a `.Add()` method, specifying both key and value:


```csharp{linenos=table,hl_lines=[],linenostart=18}
students.Add(newStudent, newGrade);
```

And while we don’t do so in this example, we may also access `Dictionary` elements using bracket notation. If we had a key/value pair of `"jesse"/4.0` in the `students` dictionary, we could access the grade with:

```csharp
double jesseGrade = students["jesse"];
```

Variables may be used to access elements:

```csharp
string name = "jesse";
double jesseGrade = students[name];
```

Looping through a dictionary is slightly more complex than it is for ordered lists. Let’s look at the `foreach` loop from this example:

```csharp{linenos=table,hl_lines=[],linenostart=30}
for (KeyValuePair<string, double> student in students) {
   Console.WriteLine(student.Key + " (" + student.Value + ")");
   sum += student.Value;
}
```

The iterator variable, student, is of type `KeyValuePair<string, double>`. The class **KeyValuePair<T,T>** is specifically constructed to be used in this fashion, to represent key/value pairs within dictionaries. Each `KeyValuePair` object has a `Key` property and a `Value` property.

If you only need to access the key of each item, you can construct a simpler loop and use the Keys property of the `Dictionary` class:

```csharp
foreach (string studentName in students.Keys) {
   Console.WriteLine(studentName);
}
```

A similar structure applies if you only need the values, using `students.Values`:

```csharp
foreach (double grade in students.Values) {
   Console.WriteLine(grade);
}
```

{{% notice blue "Note" "rocket" %}} 
We can declare and initialize a dictionary in one stroke like so:

```csharp
Dictionary<int, string> groceries = new Dictionary<int, string>
{
   {2, "Apples"},
   {3, "Oranges"},
   {1, "Avocado"}
};
```
{{% /notice %}}

## Dictionary Methods
Let’s collect some `Dictionary` methods as we have for `List`. As we said about `Lists`, this is by no means a comprehensive catalog. For full details on all properties and methods available, see the [documentation](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-6.0) on the `Dictionary` class.

For the purposes of this table, we’ll create a dictionary to hold our solar system’s planets and the number of moons associated with each.

```csharp
Dictionary<string, int> moons = new Dictionary<string, int>();
   moons.Add("Mercury", 0);
   moons.Add("Venus", 0);
   moons.Add("Earth", 1);
   moons.Add("Mars", 2);
   moons.Add("Jupiter", 79);
   moons.Add("Saturn", 82);
   moons.Add("Uranus", 27);
   moons.Add("Neptune", 14);
```

### Dictionary Methods and Properties

{{% expand `Count` %}}
   Returns the number of items in the dictionary, as an `int`.

   ```csharp
   moons.Count
   ```
   Returns `8`.
{{% /expand %}}

{{% expand `Keys` %}}
   Returns a collection containing all keys in the dictionary. This collection may be used in a `foreach` loop just as lists are, but the dictionary may not be modified within such a loop.

   ```csharp
   moons.Keys
   ``` 
   Returns `{"Earth", "Mars", "Neptune", "Jupiter", "Saturn", "Venus", "Uranus", "Mercury"}`

{{% /expand %}}

{{% expand `Values` %}}
   Returns a collection containing all values in the dictionary. This collection may be used in a foreach loop just as lists are. 
   ```csharp
   moons.Values
   ``` 
   Returns `{1, 2, 14, 79, 82, 0, 27, 0}` 
{{% /expand %}}

{{% expand `Add()` %}}
   Add a key/value pair to a dictionary. 
   ```csharp
   moons.Add("Pluto", 5)
   ```
   adds `"Pluto": 5` to the `moons`
{{% /expand %}}

{{% expand `ContainsKey()` %}}
   Returns a boolean indicating whether or not the dictionary contains a given key.       
   ```csharp
   moons.ContainsKey("Earth")
   ``` 
   Returns `true`
{{% /expand %}}

{{% expand `ContainsValue()` %}}
   Returns a boolean indicating whether or not the dictionary contains a given value.
   ```csharp
   moons.ContainsValue(79)
   ```
   Returns `true` 
{{% /expand %}}



We have only brushed the surface of how arrays, `Lists`, and dictionaries work. We leave it to you to refer to the official documentation linked below for more details. You’ll certainly be using `Lists` and dictionaries in more ways than those covered in this lesson, but with the knowledge you have now, you should be able to use C# collections and learn new uses as you go.

## Check Your Understanding

{{% notice green "Question" "rocket" %}} 
Given our `Dictionary`,

```csharp{linenos=table}
moons = {
   "Mercury" = 0,
   "Venus" = 0,
   "Earth" = 1,
   "Mars" = 2,
   "Jupiter" = 79,
   "Saturn" = 82,
   "Uranus" = 27,
   "Neptune" = 14
}
```
What is the syntax to get the key names?

1. `Dictionary.Keys(moons);`
1. `moons.Keys();`
1. `moons.Keys;`
1. `moons.KeySet();`
<!-- ans - `moons.Keys;` -->
{{% /notice %}}

{{% notice green "Question" "rocket" %}} 
Given our `Dictionary`,

```csharp{linenos=table}
moons = {
   "Mercury" = 0,
   "Venus" = 0,
   "Earth" = 1,
   "Mars" = 2,
   "Jupiter" = 79,
   "Saturn" = 82,
   "Uranus" = 27,
   "Neptune" = 14
}
```
What will moons["Mars"]; return?

1. `2`
1. `{Mars: 2}`
1. `2.0`
1. `"Mars"`
<!-- ans - ``2`` -->
{{% /notice %}}




