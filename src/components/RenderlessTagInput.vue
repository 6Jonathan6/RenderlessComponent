<script>
export default {
  model:{
    prop:'tags',
    event:'update',
  },
  props:{
    tags:{required:true},
    onBackSpace:{default:true}
  },
  data(){
    return{
      input:''
    }
  },
  computed:{
    newTag(){
      return this.input.trim()
    }
  },
  methods:{
    removeTag(tag){
      this.$emit('update',this.tags.filter(t => t !== tag))
    },
    handleBackspace(){
      if(this.newTag.length === 0){
        this.$emit('update',this.tags.slice(0, -1))
      }
    },
    addTag(){
      if(this.newTag.length === 0 || this.tags.includes(this.newTag)){
        return
      }
      this.$emit('update',[...this.tags,this.newTag])
    },

  },
  render() {
    return this.$scopedSlots.default({
      tags:this.tags,
      addTag:this.addTag,
      inputProps:{
        value:this.input
      },
      removeButtonEvents:(tag)=>({
        click:()=>{
          this.removeTag(tag)
        },
      }),
      inputEvents:{
        input: (e) => this.input = e.target.value,
        keydown:(e)=>{
          if(e.key === 'Backspace' && this.onBackSpace){
            this.handleBackspace()
          }
          if(e.key ==='Enter'){
            e.preventDefault()
            this.addTag()
          }
        }
      }
    })
  }
}
</script>
