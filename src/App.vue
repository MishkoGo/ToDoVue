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
        }
    },
    watch: {
        inputValue(value) {
            if (value.length > 10) {
                this.inputValue = ''
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
                            <button class="btn danger" @click="deleteNote(index)">Х</button>
                        </div>
                       
                    </li>
                    <hr>
                    <li>
                        <strong>Общее количество: {{ notes.length }}</strong>
                    </li>
                </ul>
                <div v-else>Заметок пока нет. Добавьте первую</div>
            </div>
        </div>
</template>
