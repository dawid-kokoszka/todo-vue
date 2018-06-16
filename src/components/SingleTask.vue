<template>
  <div class="single-task">
     <span v-show="!editable">{{value}}</span>
     <input ref="input" v-show="editable" type="text" v-model="newValue">

     <button class="btn edit" v-if="!editable" @click="isEditable"><i class="fa fa-pencil-square-o" aria-hidden="true"></i></button>
     <button class="btn edit" v-else @click="editTask"><i class="fa fa-check" aria-hidden="true"></i></button>
     <button class="btn remove-task" @click="removeTask"><i class="fa fa-trash-o" aria-hidden="true"></i></button>
     <!-- <button class="btn done"><i class="fa fa-check" aria-hidden="true"></i></button> -->

  </div>
</template>

<script>
export default {
  name: 'SingleTask',
  props:['id','value'],
  data () {
    return {
        editable: false,
        newValue: '',
    }
  },
  created(){
      this.newValue = this.value;
    
  },
  methods:{
      isEditable(){
        this.editable = true;
        let self = this
        setTimeout(function(){
            self.$refs.input.focus()
        },50)   
      },
     removeTask(){
        this.$emit('removeTask', this.id)
     },
     editTask(){

         this.$emit('updateTask', this.id, this.newValue)
         this.editable = false;
         
     }
  }
}
</script>

