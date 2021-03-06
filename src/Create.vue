<template>
    <div v-loading="loading">
        <el-form v-if="entity" ref="form" :model="entity" :rules="rules" label-width="150px" style="min-height:100px;">
            <div v-for="column in columns" :key="column">
                <slot :name="column" :entity="entity">
                    <el-crud-field :name="column" :fields="fields" :titles="titles" v-model="entity[column]"></el-crud-field>
                </slot>
            </div>
            
            <div style="margin-top:1em; text-align:right;">
                <el-button type="primary" v-on:click="submitForm()">Create</el-button>
            </div>
        </el-form>
    </div>
</template>

<script>
    import ElCrudField from './Field.vue'

    export default {
        components: { ElCrudField },
      
        props: {
          endpoint: String, 
          columns: Array,
          titles: { type: Object, default: () => { return {}; } },
          rules: { type: Object, default: () => { return {}; } },
          params: { type: Object, default: () => { return {}; } },
          fields: { type: Object, default: () => { return {}; } },
          after: { type: Function, default: null },
        },
        
        data () {
          return {
            loading: false,
            entity: null,
          }
        },
        
        created() {
            this.fetchData();
        },
              
        methods: {
          
          /**
            * Fetch data from the server
            */
          fetchData: function() {
            this.loading = true;
            
            this.$http.get(this.endpoint+'/create').then(response => {
                this.entity = response.data.entity;
                this.loading = false;
            }, response => {
                this.$notify.error( {title: 'Error', message: response.data.message });
                this.loading = false;
            });
          },
          
          /**
            * Submit the form (create entity)
            */
          submitForm: function(callback) {
            // Validate form
            this.$refs['form'].validate((valid) => {
                if (valid) {
                    this.loading = true;
                    
                    this.$http.post(this.endpoint, this.entity, { 'params': this.params }).then(response => {
                        this.data = response.data;
                        this.$notify.success( {title: 'Success', message: response.data.message });
                        this.loading = false;
                        
                        // Perform callback
                        if (this.after) {
                            this.after(this.entity);
                        }
                        
                    }, error => {
                        this.$notify.error( {title: 'Error', message: error.message });
                        this.loading = false;
                    });
                } else {
                  this.$notify.error( {title: 'Cannot submit', message: 'Form contains errors.' });
                  return false;
                }
            });
          },
        }
    }
</script>
