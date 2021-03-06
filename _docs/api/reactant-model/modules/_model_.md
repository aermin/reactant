[reactant-model](../README.md) › [Globals](../globals.md) › ["model"](_model_.md)

# External module: "model"

## Index

### Interfaces

* [Scheme](../interfaces/_model_.scheme.md)

### Type aliases

* [Actions](_model_.md#actions)
* [SerivceName](_model_.md#serivcename)

### Functions

* [model](_model_.md#const-model)

## Type aliases

###  Actions

Ƭ **Actions**: *object*

*Defined in [model.ts:11](https://github.com/unadlib/reactant/blob/222a645/packages/reactant-model/src/model.ts#L11)*

#### Type declaration:

___

###  SerivceName

Ƭ **SerivceName**: *Pick‹Service, "name"›*

*Defined in [model.ts:4](https://github.com/unadlib/reactant/blob/222a645/packages/reactant-model/src/model.ts#L4)*

## Functions

### `Const` model

▸ **model**<**S**, **A**>(`scheme`: [Scheme](../interfaces/_model_.scheme.md)‹S, A›): *[Actions](_model_.md#actions)‹A› & Service‹S› & S*

*Defined in [model.ts:15](https://github.com/unadlib/reactant/blob/222a645/packages/reactant-model/src/model.ts#L15)*

**Type parameters:**

▪ **S**: *Record‹string, any›*

▪ **A**: *Record‹string, function›*

**Parameters:**

Name | Type |
------ | ------ |
`scheme` | [Scheme](../interfaces/_model_.scheme.md)‹S, A› |

**Returns:** *[Actions](_model_.md#actions)‹A› & Service‹S› & S*
