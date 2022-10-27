<template>
    <div class="max-w-[1400px] mx-auto flex py-8 px-4">
        <input 
            v-model.lazy="value" 
            type="text"
            placeholder="Search for movie" 
            class="max-w-[350px] w-full py-3 px-2 text-base border-none"
            @keyup.enter="submit"
        />
        <button 
            v-show="value !== ''" 
            class="inline-block py-2 px-4 border-0 text-white rounded-md cursor-pointer hover:bg-yellow-700"
            @click="clear"
        >
            Clear Search
         </button>
  </div>
</template>

<script>
export default {
    props:{
        modelValue:{
            type: String,
            default: ''
        }
    },
    data(){
        return{
            value: ''
        }
    },
    watch:{
        modelValue(value){
            this.value = value
        } 
    },
    created(){
        this.value = this.modelValue
    },
    methods:{
        submit(){
            this.$emit("submitted", this.value)
        },
        clear(){
            this.$emit("clear")
        }
    }
}
</script>

<style>

</style>