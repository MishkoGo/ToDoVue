<script>
export default{
  data() {
    return {
      placeholder: 'Введите название заметки',
      title: 'Список заметок',
      inputValue: '',
      notes: [],
      checkedNotes: []
    }
  },
  methods: {
        addNewNote() {
            if(this.inputValue !== '') {
                this.notes.push(this.inputValue)
                this.inputValue = '' 
            }
        },
        toUpperCase(item){
            return item;
        },
        deleteNote(index) {
            this.notes.splice(index, 1)
        },
        editNote(index) {
            this.inputValue = this.notes[index]
            this.notes.splice(index, 1)
        }
    },
    watch: {
        inputValue(value) {
            if (value.length > 10) {
                this.inputValue = ''
            }
        },
        numbers(){
            if(this.checkedNotes) {
                this.notes.length;
            }
        }
    }
}
</script>

<template>
  <div class="container" id="app">
            <div class="card">
                <h1>{{ title }}</h1>
                <div class="form-control">
                    <input 
                        type="text" 
                        :placeholder="placeholderString" 
                        v-model="inputValue"
                        @keypress.enter="addNewNote"
                    />
                </div>
                <button class="btn" @click="addNewNote">Добавить</button>
                <hr/>
                <ul class="list" v-if="notes.length !== 0">
                    <li class="list-item" v-for="(myNote, index) in notes" :key="index">
                        <div class="input-main">
                            <input 
                                type="checkbox" 
                                class="checkbox"
                                v-model="checkedNotes[index]"
                            >
                            <span :class="['bold', { 'strikethrough': checkedNotes[index] }]">{{ toUpperCase(myNote) }}</span>
                        </div>
                        <div class="input-button">
                            <button class="btn edit" @click="editNote(index)"><svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24"><path d="M7.127 22.562l-7.127 1.438 1.438-7.128 5.689 5.69zm1.414-1.414l11.228-11.225-5.69-5.692-11.227 11.227 5.689 5.69zm9.768-21.148l-2.816 2.817 5.691 5.691 2.816-2.819-5.691-5.689z"/></svg></button>
                            <button class="btn danger" @click="deleteNote(index)">Х</button>
                        </div>
                       
                    </li>
                    <hr>
                    <li>
                        <span v-if="checkedNotes[index] !== false">Общее количество: {{ notes.length }}</span>
                    </li>
                </ul>
                <div v-else>Заметок пока нет. Добавьте первую</div>
            </div>
        </div>
</template>
