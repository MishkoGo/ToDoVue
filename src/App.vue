<script>
export default{
  data() {
    return {
      placeholder: 'Введите название заметки',
      title: 'Список заметок',
      inputValue: '',
      notes: ['Заметка 1', 'Заметка 2']
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
            return item.toUpperCase()
        },
        deleteNote(index) {
            this.notes.splice(index, 1)
        }
    },
    computed: {
        doubleCountComputed() {
            console.log('doubleCountComputed')
            return this.notes.length * 2
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
                    <li class="list-item" v-for="(myNote, index) in notes" :key="myNote">
                        
                        <span :class="['bold', {'primary': myNote.length > 5}]">{{ toUpperCase(myNote) }}</span>
                        <button class="btn danger" @click="deleteNote(index)">Удалить</button>
                    </li>
                    <hr>
                    <li>
                        <strong>Общее количество: {{ notes.length }}</strong> | Удвоенное: {{ doubleCountComputed }}
                    </li>
                </ul>
                <div v-else>Заметок пока нет. Добавьте первую</div>
            </div>
        </div>
</template>
