# Element-UI CRUD

CRUD components for Element-UI (Vue).

## Installation

```
$ npm install element-ui-crud --save
```


## Example Usage

```vue
<template>
    <div>
        <h1>IDX - Dataflows</h1>
        <hr/>
        
        <el-crud :endpoint="'/api/users"
                  primary-key="id"
                  :list="['id', 'name']"
                  :create="['name']"
                  :edit="['name']"
                  :titles="{ 'id': 'ID', 'name': 'Name' }"
                  :order="{'name': 'ASC'}"
                  :pagination="50"
                  :show-refresh="false">
          <template slot="list" scope="scope">
              <el-button size="small" type="primary" v-on:click="alert(scope.row)" icon="information"></el-button>
          </template>
        </el-crud>
    </div>
</template>

<script>
    import ElCrud from "element-ui-crud"

    export default {
        components: { ElCrud },
    }
</script>
```

## Components

Element-UI CRUD is designed to be modular so that each component can be used on its own.

### ElCrud

The primary component that provides full CRUD functionality.

#### Parameters

- endpoint
    **Type:** string
    **Example:** "/api/users"
    **Description:**
    The root HTTP REST endpoint of your backend that provides CRUD functionality.
    Note that this should implement the same endpoints as Laravel's Resource Controller.

- primary-key (optional)
    **Type:** string
    **Default:** "id"
    **Example:** "id"
    **Description:**
    The primary key to use on the List component.

- list
    **Type:** array
    **Example:** ["id", "name"]
    **Description:**
    Fields that should be shown on the List component.

- create
    **Type:** array
    **Example:** ["name"]
    **Description:**
    Fields that should be shown on the Create component.
    If not specified, create functionality will not be offered.

- edit
    **Type:** array
    **Example:** ["name"]
    **Description:**
    Fields that should be shown on the Edit component.
    If not specified, edit functionality will not be offered.

- edit
    **Type:** array
    **Example:** ["name"]
    **Description:**
    Fields that should be shown on the Edit component.
    If not specified, edit functionality will not be offered.

- show-delete
    **Type:** boolean
    **Default:** true
    **Example:** true
    **Description:**
    Whether "Delete" should be shown next to items in row.

- show-refresh
    **Type:** boolean
    **Default:** true
    **Example:** true
    **Description:**
    Whether "Refresh" button should be shown above table.

- titles
    **Type:** Object
    **Example:** { id: 'ID', name: 'Name' }
    **Description:**
    Titles to apply to List Columns and Create/Edit Forms.
    If not provided, the key for that column is used.

- order (TODO)
    **Type:** Object
    **Example:** { id: 'ID', name: 'Name' }
    **Description:**
    Titles to apply to List Columns and Create/Edit Forms.
    If not provided, the key for that column is used.

- params
    **Type:** Object
    **Example:** { level: 'admin' }
    **Description:**
    Extra parameters that should be passed with every request.
    Can be used for filtering the results server-side.

- fields (TODO)
    **Type:** Object
    **Example:** { level: 'admin' }
    **Description:**
    Extra parameters that should be passed with every request.
    Can be used for filtering the results server-side.

- after
    **Type:** function
    **Example:** function(entity) { this.$store.dispatch('refreshUsers'); }
    **Description:**
    Function to perform after Create/Edit.
    For example, after a edit is performed, you might wish to update a VueX store.

- pagination
    **Type:** integer
    **Default:** 0
    **Example:** 50
    **Description:**
    If set, Pagination will be enabled. This must be handled server-side.
    (TODO)

- create-size
    **Type:** string
    **Default:** "small"
    **Example:** "large"
    **Description:**
    Size of the Create Dialog.

- edit-size
    **Type:** string
    **Default:** "small"
    **Example:** "large"
    **Description:**
    Size of the Edit Dialog.

- delete-size
    **Type:** string
    **Default:** "tiny"
    **Example:** "small"
    **Description:**
    Size of the Delete Dialog.

### ElList

Component to display the Rows in a table.

### ElEdit

Component to display the Edit Form.

### ElCreate

Component to display the Create Form.

## Badges

![](https://img.shields.io/badge/license-MIT-blue.svg)
![](https://img.shields.io/badge/status-dev-yellow.svg)

---
