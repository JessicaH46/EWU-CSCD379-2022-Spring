<template>
   <v-card>
    <v-dialog
      v-model="dialog"
      scrollable
      max-width="300px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn 
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
          @click="show2"
        >
          Available
        </v-btn>
      </template>
      <v-card>
        <v-card-title>Select Word</v-card-title>
        <v-divider></v-divider>
        <v-card-text style="height: 300px;">
        <v-list>
            <v-list-item
                v-for="x in matchesArray"
                :key="x"
                @click="emit(x)"    
            >
            </v-list-item>
        </v-list>
        </v-card-text>
        <v-divider></v-divider>
      </v-card>
    </v-dialog>
   </v-card>
</template>

<script lang="ts">

//import { defineComponent } from 'vue'
import { Component, Vue, Prop } from 'vue-property-decorator'
import { WordsService } from '~/scripts/wordsService'
import { Word } from '~/scripts/word'

@Component({})
export default class WordList extends Vue { //make word list class
    //@Prop({required: true})
    //matchesArray!: string[]
    @Prop({required: true})
    //show: boolean = false
    show!: boolean
    @Prop({required: true})
    off!: boolean

    emit(x: string){
        this.$emit('fill-word', x)
        this.conceal()
    }

    conceal(){
        this.show = false
    }

    show2(){
        this.show = true
    }


    //matchesArray: string [] = WordsService.validWords();

}
</script>
