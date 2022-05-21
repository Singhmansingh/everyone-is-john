<template>
  <div id="container">
    <div id="john-voice">
      <div id="voice-container">
        <div id="name-container" class="section">
          <h3>You are:</h3>
          <p contenteditable="true" spellcheck="false">{{voiceName}}</p>
        </div>
        <div id="skills-container" class="section">
          <h2 @click="toggleThirdSkill" title="click here to toggle third skill. If you use 3 skills, your starting willpower is 7.">Skills</h2>
          <p contenteditable="true" class="skill" v-for="(skill, index) in skills" :key="'skill-'+index">{{skill}}</p>
        </div>
         <div id="obsessions-container" class="section">
          <h2>Obsessions <span class="score" v-on:click.left="obsessionScore++" v-on:click.right="obsessionScore--" @contextmenu="e => e.preventDefault()">{{obsessionScore}}</span></h2>
          <div class="obsession" v-for="(obsession, index) in obsessions" :key="'obsession-'+index">
            <p>Level {{index+1}}:</p>
            <p contenteditable="true" class="obsessionText">{{obsession}}</p>
          </div>
        </div>
      </div>
    </div>
    <div id="middle-container">
      <div id="picture-container">
        <img src="../assets/John.png"/>
      </div>
      <div id="willpower-container">
        <div class="box" @click="reduceWill" v-on:click.right="increaseWill" @contextmenu="e => e.preventDefault()">
          <h2>Remaining Willpower</h2>
          <p>{{willpower}}</p>
        </div>
      </div>
    </div>
    <div id="other-voice-notes">
      <EditorComponent/>
    </div>

  </div>
</template>

<script>
import EditorComponent from './EditorComponent.vue'

export default {
  name: 'GameScreen',
  components:{
    EditorComponent
  },
  data(){
    return {
      voiceName:"John",
      skills:["Skill 1", "Skill 2"],
      obsessions: ["Simple Task to acieve", "Bit harder, but realistically achievable", "Very Difficult to achieve"],
      obsessionScore: 0,
      willpower: 10,
    }
  },
  methods:{
    reduceWill(){
      if(this.willpower > 0) this.willpower--;
    },
    increaseWill(){
      if((this.willpower < 10 && this.skills.length != 3) || (this.willpower < 7 && this.skills.length >= 3)) this.willpower++;
    },
    toggleThirdSkill(){
      if(this.skills.length >= 3) {
        this.skills.pop()
        this.willpower = 10
      }
      else {
        this.skills.push("Skill 3")
        this.willpower = 7
        }
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">

$borderWidth: 10px
$grey: #414141


@mixin border()
  border: 3px solid $grey
  border-radius: 5px
#container
  background: white
  flex: 1
  height: 100%
  display: flex
  flex-direction: row
  h2
    font-size: 1.7rem
    margin: 0
    margin: 7px
  h3
    margin: 4px
  #john-voice
    flex: 1
    padding: 10px
    #voice-container
      box-sizing: content-box
      height: 100%
      display: flex
      flex-direction: column

      #name-container
        border-top-left-radius: $borderWidth
        border-top-right-radius: $borderWidth
        border-bottom: none
        background: $grey
        color: white
        flex-shrink: 1
        padding: 20px
        p
          font-size: 2.4rem
          font-weight: bold
          margin: 0
      #skills-container
        flex: 2
        display: flex
        padding: 10px
        justify-content: space-evenly
        flex-direction: column
        border-bottom: none
        h2
          cursor: pointer
          user-select: none
        .skill
          @include border()
          
          font-size: 1.2em
          
          height: 50px
          display: inline-flex
          justify-content: center
          align-items: center
          padding: 10px
          margin: 10px

      #obsessions-container
        flex: 3
        padding: 10px
        display: flex
        flex-direction: column
        border-bottom-left-radius: $borderWidth
        border-bottom-right-radius: $borderWidth
        h2
          flex-shrink: 1
          .score
            background: $grey
            cursor: pointer
            user-select: none
            padding-left: 15px
            padding-right: 15px
            color: white
            box-sizing: border-box
            @include border()
        .obsession
          flex: 1
          display: flex
          justify-content: flex-start
          flex-direction: column
          align-items: center
          font-size: 1.2em
          padding: 10px
          p
            flex: 1
            margin: 0
            text-overflow: ellipsis
          .obsessionText
            width: 100%
            max-width: 100%
            display: inline-flex
            font-size: 0.8em
            justify-content: flex-start
            padding-left: 10px
            box-sizing: border-box
            align-items: center
            @include border()
      .section
        border: 3px solid black
        
  #middle-container
    flex: 2
    width: 100%
    display: flex
    flex-direction: column
    padding: 10px
    #picture-container
      flex: 2
      background: #797979
      display: flex
      flex-direction: column
      justify-content: flex-end
      align-items: center
      background-image: url('../assets/background.png')
      background-position: center
      background-size: cover
      background-blend-mode: screen

      img
        height: 90%
        
    #willpower-container
      flex: 1
      padding: 10px
      box-sizing: border-box
      cursor: pointer
      user-select: none
      .box
        width: 100%
        height: 100%
        @include border()
        display: flex
        flex-direction: column
        h2
          flex: 1
          justify-content: center
          align-items: center
          font-size: rem
          display: flex
          margin: 10px
        p
          flex: 3
          display: flex
          font-size: 9em
          margin: 0
          justify-content: center
          background: #414141
          color: white
          align-items: center

  #other-voice-notes
    display: flex
    flex: 1
    flex-direction: column
    box-sizing: border-box
    padding: 10px


//editor 

</style>
