<script>
import worD from './Word.vue'
// import meanIng from './Meaning.vue'
import axios from "axios";
export default {
    name: 'HoMe',
    data() {
        return {
            Word: null,
            title: 'Dictionary WebApp',
            wordMean:[],
            errorMessage:"",
            isLoading:false
        }
    },
    methods: {
        async getData(word) {
            this.isLoading = true; //show laoder
            console.log("values: ", this.Word);
            try{
            const response = await axios.get(`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`)
            console.log("Response: ",response)
            console.log(this.wordMean)
            this.wordMean = response.data;
            this.errorMessage="";
            }
            catch(error){
                console.error("Error in fetching data: ",error);
                if(error.response && error.response.status ===400){
                    this.errorMessage="Word Not Found!";
                }
                else{
                    this.errorMessage = "An error occurred!";
                }
                this.wordMean=null;
               
            } finally{
                this.isLoading = false; // hide loader
            }
        },
        reset(){
            this.Word=null;
            this.wordMean=null;
            console.warn("Reset invoke!",this.wordMean);
        }
    },
    components:{
        worD
    }
}
</script>

<template>
    <div class="container text-center">
        <h1 class="pb-2 mb-3 text-grey border-bottom border-info">{{ title }}</h1>
        <input type="text" placeholder="Enter any word"
            class="rounded border mt-4 w-50 p-3 bg-info-subtle text-info-emphasis shadow-lg p-3 mb-5 bg-body-tertiary"
            v-model="Word">
        <button type="button" class="rounded p-2 mx-3 btn btn-outline-info" @click="getData(Word)">Search</button>
        <button type="button" class="rounded p-2 mx-3 btn btn-outline-danger" @click="reset()">Reset</button>
        <h2 class="text-start">{{ this.Word }}</h2>

    </div>

    <div class="contanier-sm">
        <worD :Word="Word" :wordMean="wordMean" :errorMessage="errorMessage" :isLoading="isLoading"/>
       
        
    </div>
    <!-- <span v-html="error" v-else></span> -->
</template>