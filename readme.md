## Introduction

`objection-gen` generates random data for [Objection.js](https://github.com/Vincit/objection.js/)'s model and other related models.
It uses a model's `jsonSchema` and `relationMappings`to generate random
data and follow the relations respectively. Internally it uses
[json-schema-faker](https://github.com/json-schema-faker/json-schema-faker)
for generating fake data.

## Installation
Using npm
```
npm install -s objection-gen
```

Using yarn
```
yarn add objection-gen
```

## Supported db
- psql
- mysql

## Walkthrough
The best Walkthough is the tests in the repo.
Checkout the [tests](https://github.com/ludbek/objection-gen/blob/master/index.test.js)
to learn how it can be used.

## API
### 1. create(model: ObjectionModel, overrides: object, options: object)
#### 1.1. model
It is an Objection model with `jsonSchema`.

#### 1.2. overrides
It is an object used for overriding generated data.
For example, `create(Account, {username: 'ausername'})` will generate
random data for all columns except for `username`.

#### 1.3. options
Default value of options `{followRelations: true}`
Set `followRelations` to `false` if we do not want to insert related models.


### 2. clean()
It truncates the tables populated using `create` function.
Internally `objection-gen` keeps the list of dirty tables.
One can add new dirty table using `addDirtyModel` function if the table
is being populated through other means. After that `clean` will truncate
those tables too.

### 3. prepare(model: ObjectionModel, overrides: object)
It returns the random data for a model but does not inserts in to the db.
The data returned by it is flat which means it does not follow the relations.

### 4. addDirtyModel(model: ObjectionModel)
It adds a model to `objection-gen`'s internal list of dirty models.
Use it if one wishes to use `clean()` for truncating dirty models that
are being populated manually.

