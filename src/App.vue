<template>
<div id="app" class="min-h-screen bg-grey-darker p-8">
    <div class="max-w-sm mx-auto card mt-8">

      <label class="form-label mb-2">Renderless Stacked Layout</label>
      <renderless-tag-input v-model="tags" :on-back-space="false">
        <div class="stacked-tag-input" slot-scope="{ tags, addTag, removeButtonEvents, inputProps, inputEvents }">
          <div class="stacked-tag-input-form">
            <input v-bind="inputProps" v-on="inputEvents" class="form-input" placeholder="Add tag...">
            <button class="btn btn-indigo" @click="addTag">Add tag</button>
          </div>
          <ul class="stacked-tag-list">
           <li v-for="tag in tags" :key="tag">
             {{ tag }}
             <button v-on="removeButtonEvents(tag)" type="button" class="stacked-tag-link">
               Remove
             </button>
           </li>
          </ul>
        </div>
      </renderless-tag-input>
    </div>
    <div class="max-w-sm mx-auto card mt-8">
      <label class="form-label mb-2">Renderless Tag Input</label>
      <renderless-tag-input v-model="tags">
        <div class="tag-input" slot-scope="{ tags, removeButtonEvents, inputProps, inputEvents }">
          <span v-for="tag in tags" class="tag-input-tag" :key="tag">
            <span>{{tag}}</span>
            <button v-on="removeButtonEvents(tag)" type="button" class="tag-input-remove"
            >&times;</button>
          </span>
          <input class="tag-input-text" placeholder="Add tag..."
            v-bind="inputProps"
            v-on="inputEvents"
          >
        </div>
      </renderless-tag-input>

    </div>


    <div class="max-w-sm mx-auto card mt-8">
      <label class="form-label mb-2">Original Tag Input</label>
      <tag-input v-model="tags"></tag-input>
    </div>
  </div>


</template>

<script>
import TagInput from './components/TagInput.vue'
import RenderlessTagInput from './components/RenderlessTagInput.vue'
export default {
  name: 'app',
   components: {
    TagInput,
    RenderlessTagInput,
  },
  data(){
    return {
       tags: ['awesome', 'excellent', 'amazing'],
    }
  }
}
</script>
<style src="./assets/css/app.css"/>
<style>
  input{
    background-color: azure;
  }
</style>
