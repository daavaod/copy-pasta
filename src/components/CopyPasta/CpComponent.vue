<template>
    <div class="cp-container">
        <ul>
            <CpItem v-for="item in cpDataLocal" :key="item.id" :itemData="item" @emitInput="handleEmitInput" @emitDelete="handleEmitDelete" @emitChange="handleEmitChange"/>
        </ul>
        <div>
            Text in clipboard: {{ copiedText }}
        </div>
        <div>
           cpDataLocal: {{ cpDataLocal }}
        </div>
        <div>
            <button @click.prevent="handleCreate">Create new item</button>
        </div>
    </div>
</template>

<script>
import cpData from '../../scripts/cp-data.js'
import CpItem from './CpItem.vue'
import CpGenerate from './CpGenerate.vue'

export default {
    name: "CpContainer",
    components: {
        CpItem,
        CpGenerate
    },
    props: {

    },
    data() {
        return {
            copiedText: '',
            cpDataLocal: null
        }
    },
    computed: {
        
    },
    methods: {
        handleEmitInput(val) {
            this.copiedText = val;
        },
        handleEmitDelete(val) {
            let getLS = JSON.parse(localStorage.getItem('cpData'));

            let removeItem = getLS.filter(item => {
                return item.id !== val
            })

            localStorage.setItem('cpData', JSON.stringify(removeItem))

            this.getCpLocalStorage();

        },
        handleEmitChange(val) {
            this.handleUpdate(val.id, val.text);
        },
        generateId() {
            return Math.floor(Math.random() * 10000);
        },
        handleUpdate(id, text) {
            let getLS = JSON.parse(localStorage.getItem('cpData'));

            let updateItem = getLS.map(item => {
                if(item.id === id) {
                    let newItem = {
                        id: item.id,
                        text: text
                    }
                    return newItem
                } else {
                    return item
                }
            })

            localStorage.setItem('cpData', JSON.stringify(updateItem))

            this.getCpLocalStorage();
        },
        handleCreate() {
            let generateId = this.generateId()
            let getLS = JSON.parse(localStorage.getItem('cpData'));

            let payload = {
                id: generateId,
                text: ''
            }

            getLS.push(payload);

            localStorage.setItem('cpData', JSON.stringify(getLS))

            this.getCpLocalStorage();
        },
        setLocalStorage(value) {
            let getCurrent = this.getCpLocalStorage();

            localStorage.setItem('cpData', JSON.stringify())
        },
        getCpLocalStorage() {
            let cpDataLocal = localStorage.getItem('cpData');

            if(cpDataLocal) {
                this.cpDataLocal = JSON.parse(cpDataLocal);
            } else {

                let payload = [{
                    id: this.generateId(),
                    text: ''
                }]

                localStorage.setItem('cpData', JSON.stringify(payload))
            }
        }
    },
    created() {
        this.getCpLocalStorage();
    }
};
</script>

<style>
    
</style>