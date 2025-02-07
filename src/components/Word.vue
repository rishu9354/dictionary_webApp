<script>
export default{
    name:'worD',
    props:{
        Word:String,
        wordMean:[],
        errorMessage:String,
        isLoading:Boolean
    },
    data(){
        return{
            wordData:[]
        }
    },


}
</script>

<template>
    <div v-if="isLoading">
        Loading ....
    </div>
    <div v-if="errorMessage">
        <p>{{ errorMessage }}</p>
    </div>


   <!-- for one menaing -->
    <div class="container" v-for="item in wordMean" :key="item.meanings">
        <span>{{ item.phonetics[0].text }}</span>
       <!-- <span><audio :src="item.phonetics[0]?.audio" controls></audio></span>  -->
        <span class="mx-2">{{ item.meanings[0].partOfSpeech }}</span>
        <h5>Definition:</h5>
        <ol>
            <li>{{ item.meanings[0].definitions[0].definition }}</li>
            <!-- <li>{{ item.meanings[1].definitions[0].definition }}</li> -->

        </ol>
        <h5>Example:</h5>
        <ol>
            <li>{{ item.meanings[0].definitions[0].example }}</li>
            <!-- <li>{{ item.meanings[1].definitions[0].example }}</li> -->
        </ol>

    </div>

</template>