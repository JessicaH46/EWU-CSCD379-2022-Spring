<template>
  <v-card width="450"
  style = "background: linear-gradient(180deg, rgba(5,50,85,.5) 0%, rgba(5,50,90,1) 85%, rgba(10,50,110,1) 100%)">
    <v-container>
      <v-row v-for="row in wordleGame.maxGuesses" :key="row" dense>
        <v-col v-for="index in wordleGame.currentWord.maxLetters" :key="index">
          <v-card height="50" :color="letterColor(getLetter(row, index))">
            <v-card-text class="text-center">
              {{ getChar(getLetter(row, index)) }}
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator'
import { WordleGame } from '~/scripts/wordleGame'
import { Word } from '~/scripts/word'
import { Letter } from '~/scripts/letter'

@Component({ components: {} })
export default class GameBoard extends Vue {
  @Prop({ required: true })
  wordleGame!: WordleGame

  getLetter(row: number, index: number): Letter | null {
    const word: Word = this.wordleGame.words[row - 1]
    if (word !== undefined) {
      return word.letters[index - 1] ?? null
    }
    return null
  }

  getChar(letter: Letter | null) {
    if (letter === null) return ''
    return letter.char
  }

  letterColor(letter: Letter | null): string {
    if (letter === null) return ''
    return letter.letterColor
  }
}
</script>
