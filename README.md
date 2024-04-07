# Advanced TypeScript Topics

This repository contains the practical examples of advanced typescript topics.

## Table of Contents

- [Enums](##Enums)

## Enums

### Introduction

Enums short for enumerations are used to define a set of named constants, aiding in readability and maintainability by avoiding "magic numbers" or "magic strings." They support both numeric and string-based values, facilitating easy conversion between values and their associated names. This feature makes enums a valuable tool for organizing and managing constant values in TypeScript projects.

### Why-Enums

In Javascript we can declare constants using `const` keyword but things can get messy if we have to set constant values for alot of closely related values.

```
const male = 'male';
const female = 'female';
const others = 'others';
```

Here we can see that we need three different variables but we can replace it with single `enum`

```
enum Gender {
    male,
    female,
    others
}
```

### Default-Values

By default all the variables inside an enum will have values equal to there indicies.

```
console.log(Gender.male); // 0
console.log(Gender.female); // 1
console.log(Gender.others); // 2
```

### Change Default Values

We need to provide values while defining an enum to change default values.

```
enum Gender {
    male = 2
    female
    others
}
```

Surprisingly, now the indicies will start from 2.

```
console.log(Gender.male); // 2
console.log(Gender.female); // 3
console.log(Gender.others); // 4
```

We can set any values

```
enum Gender {
    male = 2
    female = 10
    others = 8
}
```

```
console.log(Gender.male); // 2
console.log(Gender.female); // 10
console.log(Gender.others); // 8
```

### Linking Items in an Wnum

We can even link one value to the other

```
enum Gender {
    male = 2
    female = male + 1
    others = female + 2
}
```

```
console.log(Gender.male); // 2
console.log(Gender.female); // 3
console.log(Gender.others); // 5
```

### Computed Values

Functions to provide computed values

```
const addOneToCurrent = (value: number) => value + 1;
```

```
enum Gender {
    male = 2
    female = male + 1
    others = addOneToCurrent(female)
}
```

```
console.log(Gender.male); // 2
console.log(Gender.female); // 3
console.log(Gender.others); // 4
```

### Optimization

One optimization trick is to add `const` before defining `enum`. This allows for a much smaller compiled JS.

```
const enum Gender {
    male = 2
    female = male + 1
    others = addOneToCurrent(female)
}
```

### Downside of Enums

One downside of `enums` is that they are not portable. Say your one project uses typescript and other uses javascript, you can't use code from one in the other. To increase portability we can use a simple trick.

```
const gender = {
    male: 'male',
    female: 'female',
    others: 'others'
} as const
```

```
console.log(gender.male); // 'male'
console.log(gender.female); // 'female'
console.log(gender.others); // 'others'
```

As this a object now but `as const` make it impossible to add or change any of the properties just like `enums`.
