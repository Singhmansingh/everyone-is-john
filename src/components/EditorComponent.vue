<template>
    <div v-if="editor" class="controls">
          <button @click="editor.chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }">
            Bold
          </button>
          <button @click="editor.chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }">
            Italic
          </button>
          <button @click="editor.chain().focus().toggleStrike().run()" :class="{ 'is-active': editor.isActive('strike') }">
            Strike
          </button>
          <button @click="editor.chain().focus().setParagraph().run()" :class="{ 'is-active': editor.isActive('paragraph') }">
            Paragraph
          </button>
          <button @click="editor.chain().focus().toggleHeading({ level: 1 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }">
            Heading
          </button>
        
          <button @click="editor.chain().focus().toggleBulletList().run()" :class="{ 'is-active': editor.isActive('bulletList') }">
            bullet list
          </button>
          <button @click="editor.chain().focus().toggleOrderedList().run()" :class="{ 'is-active': editor.isActive('orderedList') }">
            ordered list
          </button>
        
          <button @click="editor.chain().focus().setHorizontalRule().run()">
            divider bar
          </button>
          <button class="undo-redo" @click="editor.chain().focus().undo().run()">
            undo
          </button>
          <button class="undo-redo" @click="editor.chain().focus().redo().run()">
            redo
          </button>
  </div>
      <EditorContent :editor="editor" class="editor"/>
</template>

<script>
import { useEditor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

export default {
    name:"EditorComponent",
 components:{
    EditorContent,
  },
   setup() {
    const editor = useEditor({
      content: '<h1>I am the only John!</h1><p>But someone else is trying to take control...</p><code>Use this area to make notes on the other Johns!</code>',
      extensions: [
        StarterKit,
      ],
    })

    return { editor }
  },
}
</script>

<style lang="sass" scoped>
$borderRadius: 10px
$grey: #414141
.controls
  display: flex
  justify-content: center
  padding: 10px 0 10px 0
  flex-shrink: 1
  background: #414141
  overflow: hidden
  border-top-left-radius: $borderRadius
  border-top-right-radius: $borderRadius
  flex-wrap: wrap
  gap: 10px
  border: 3px solid $grey
  border-bottom-width: 0
  .undo-redo
    background: #6c6c6c
    color: white
  button
   background: white
   border: 2px solid $grey
   min-width: 80px
   padding: 10px
   border-radius: $borderRadius
   font-family: inherit
   &:hover
    cursor: pointer 
    

.editor
  flex: 1  
  background: white
  text-align: left
  overflow-y: auto
  overflow-x: clip
  padding: 20px
  height: 100%
  border-bottom-left-radius: $borderRadius
  border-bottom-right-radius: $borderRadius
  border: 3px solid $grey

.ProseMirror 
  > * + * 
    margin-top: 0.75em
  

  ul,
  ol 
    padding: 0 1rem
  
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 
    line-height: 1.1
  

  code 
    background-color: rgba(#616161, 0.1)
    color: #616161
  

  pre 
    background: #0D0D0D
    color: #FFF
    font-family: 'JetBrainsMono', monospace
    padding: 0.75rem 1rem
    border-radius: 0.5rem

    code 
      color: inherit
      padding: 0
      background: none
      font-size: 0.8rem
    
  

  img 
    max-width: 100%
    height: auto
  

  blockquote 
    padding-left: 1rem
    border-left: 2px solid rgba(#0D0D0D, 0.1)
  

  hr 
    border: none
    border-top: 2px solid rgba(#0D0D0D, 0.1)
    margin: 2rem 0
  

</style>