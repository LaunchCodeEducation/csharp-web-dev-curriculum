---
title: "Exercises"
date: 2023-01-25T13:23:58-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Work on these exercises in your local copy of the [csharp-web-dev-unittesting](https://github.com/LaunchCodeEducation/csharp-web-dev-unittesting) repo.
You were directed to fork and clone this repo earlier in the chapter. If you have not done so, do so now.
Before starting work on the exercises, check out the `exercises-start` branch.

{{% notice green "Tip" "rocket" %}}

   Earlier in the chapter, we instantiated an object of the `Car` class called `test_car`.
   Be sure to take note of the values of the `make`, `model`, `gasTankSize`, and `milesPerGallon` fields!
   Having a note you can quickly reference of how big the gas tank is will help you decide on values to use in your tests!

{{% /notice %}}

## `TestGasTankAfterDriving()`

Add a test for the third TODO, "GasTankLevel is accurate after driving within tank range".

1. Your test must use the `Car` method `Drive()`

   ```csharp
      test_car.Drive(50);
   ```

1. With a value of `50` miles passed into `Drive()`, we expect `test_car` to have a `GasTankLevel` of `9`.

   ```csharp
      Assert.AreEqual(9, test_car.GasTankLevel, .001);
   ``` 

   {{% expand "Click Here for Answer" %}}

   ```csharp {linenos = table}
      //TODO: GasTankLevel is accurate after driving within tank range
      [TestMethod]
      public void TestGasTankAfterDriving()
      {
         test_car.Drive(50);
         Assert.AreEqual(9, test_car.GasTankLevel, .001);
      }
   ```

   {{% /expand %}}

## `TestGasTankAfterExceedingTankRange()`

Add a test for the fourth TODO, "GasTankLevel is accurate after attempting to drive past tank range".

1. You're on your own for this one. You'll need to simulate the `Car` traveling farther than it's `gasTankLevel` allows.

   {{% expand "Click Here for Answer" %}}

   ```csharp {linenos = table}
      //TODO: GasTankLevel is accurate after attempting to drive past tank range
        [TestMethod]
        public void TestGasTankAfterExceedingTankRange()
        {
            test_car.Drive(501);
            Assert.AreEqual(test_car.GasTankLevel, 0, .001);
        }
   ```

   {{% /expand %}}

## `TestGasOverfillException()`

The test for our last TODO is a little different. We are going to 
perform an action on our car object, and we are expecting the object 
to throw an error. In this case, we are going to attempt to add gas 
to our car that exceeds the gas tank size.

1. First, we'll add our `[TestMethod]` annotation to tell MSTest this is a test. 

   ```csharp
      //TODO: can't have more gas than tank size, expect an exception
      [TestMethod]
      public void TestGasOverfillException() {

      }
   ```

2. Now we need to tell MSTest the test passes if an exception is thrown. We will use a new attribute `[ExpectedException]`.

   ```csharp
      [ExpectedException(typeof(ArgumentOutOfRangeException))]
   ```

   {{% expand "Click Here for Answer" %}}

   ```csharp {linenos = table}
      //TODO: can't have more gas than tank size, expect an exception
      [TestMethod]
      [ExpectedException(typeof(ArgumentOutOfRangeException))]
      public void TestGasOverfillException()
      {

      }
   ```

   {{% /expand %}}

3. Update the `Car` class to include an `AddGas()` method.

   ```csharp
      public void AddGas(double gas) {
        GasTankLevel += gas;
      }
   ```

4. Back in `CarTests`, implement the new `AddGas()` method and a `Assert.Fail()` scenario.

   ```csharp
      test_car.AddGas(5);
      Assert.Fail("Shouldn't get here, car cannot have more gas in tank than the size of the tank");
   ```

   {{% expand "Click Here for Answer" %}}

   ```csharp {linenos = table}
      //TODO: can't have more gas than tank size, expect an exception
      [TestMethod]
      [ExpectedException(typeof(ArgumentOutOfRangeException))]
      public void TestGasOverfillException()
      {
         test_car.AddGas(5);
         Assert.Fail("Shouldn't get here, car cannot have more gas in tank than the size of the tank");
      }
   ```

   {{% /expand %}}

5. Run the test. It should fail! In the output log, we can see our `Assert.Fail()` statement about not being able to add more gas printed out.

6. We need to refactor `Car` to throw an exception when too much gas is added to the tank. Find the `AddGas()` method and modify it by adding the following code in the appropriate place.

   ```csharp 
      if (GasTankLevel > GasTankSize)
      {
         throw new ArgumentOutOfRangeException("Can't exceed tank size");
      }
   ```

   {{% expand "Click Here for Answer" %}}

   ```csharp {linenos = table}
      public void AddGas(double gas)
      {
         GasTankLevel += gas;
         if (GasTankLevel > GasTankSize)
         {
            throw new ArgumentOutOfRangeException("Can't exceed tank size");
         }
      }
   ```

   {{% /expand %}}

7. Now, run the test - it should pass!