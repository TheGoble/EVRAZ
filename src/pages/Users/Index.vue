<template>
  <q-page>
        <div class="q-pa-md">
        <div>
            <q-btn class="button" color="secondary" @click="showWindow">Добавить пользователя</q-btn>
            <q-dialog v-model="showDialog" @before-hide="closeWindow">
            <q-card>
                <q-card-section class="add_user">
                   Добавьте пользователя
                </q-card-section>
                <q-card-section>
                    <q-input class="input_email" standout="bg-secondary text-white" v-model="message.email" label="Email" />
                    <q-input class="input_phone" standout="bg-secondary text-white" v-model="message.phone" label="Номер телефона" />
                    <q-input class="input_FIO" standout="bg-secondary text-white" v-model="message.FIO" label="ФИО" />
                    <q-input class="input_workshop" standout="bg-secondary text-white" v-model="message.workshop" label="Номер цеха" />
                    <q-input class="input_line" standout="bg-secondary text-white" v-model="message.line" label="Номер участка" />
                    <div class="q-pd-md">
                        <div class="q-gutter-sm">
                            <q-checkbox color="secondary" v-model="message.chief_workshop" label="Начальник цеха" />
                            <q-checkbox color="secondary" v-model="message.chief_line" label="Начальник участка" />
                        </div> 
                    </div>
                </q-card-section>
                <q-card-actions>
                <q-btn color="secondary" label="Закрыть" @click="closeWindow" />
                <q-btn class="button_add" color="secondary" label="Добавить" @click="addMessage"></q-btn>
                </q-card-actions>
            </q-card>
            </q-dialog>
        </div>
        <q-table
            title="Список пользователей"
            :data="data"
            :columns="columns"
            row-key="name"
        />
        </div>  
    </q-page>
</template>

<script>
export default {
    data () {
    return { 
        chief_workshop: false,
        chief_line: false,
        showDialog: false,
        data: [],
        message: {
            email: '',
            phone: '',
            FIO: '',
            workshop: '',
            line: '',
            chief_workshop: false,
            chief_line: false,
        },
        columns: [
            {
            name: 'name',
            required: true,
            label: 'Номер',
            align: 'left',
            field: row => row.name,
            format: val => `${val}`,
            },
            { name: 'email', align: 'center', label: 'Email', field: 'email'} ,
            { name: 'Phone', align: 'center', label: 'Номер телефона', field: 'phone'},
            { name: 'FIO', align: 'center', label: 'ФИО', field: 'FIO' },
            { name: 'Number_shop', align: 'center', label: 'Номер цеха', field: 'workshop' },
            { name: 'Number_line', align: 'center', label: 'Номер участка', field: 'line' },
            { name: 'chief_workshop', align: 'center', label: 'Начальник цеха', field: 'chief_workshop', format: value => value ? 'Да' : 'Нет' },
            { name: 'chief_line', align: 'center', label: 'Начальник участка', field: 'chief_line', format: value => value ? 'Да' : 'Нет'  },
        ],
    };
    },
    methods: {
        showWindow() {
        this.showDialog = true;
        },
        closeWindow() {
        this.showDialog = false;
        this.message.email = '';
        this.message.phone = '';
        this.message.FIO = '';
        this.message.workshop = '';
        this.message.line = '';
        this.message.chief_workshop = false;
        this.message.chief_line = false;
        },
        addMessage() {
            this.data.push({
                name: this.data.length + 1,
                ...this.message,
            })
            this.closeWindow();
        },
    },
}
</script>

<style> 
.add_user{
    font-family: inherit;
    font-size: 2vh;
}
.q-pd-md{
    font-family: inherit;
    font-size: 2vh;
}
.button{
    margin-top: 3vh;
    margin-bottom: 5vh;
}
.input_email{
    margin-bottom: 2vh;
}
.input_phone{
    margin-bottom: 2vh;
}
.input_FIO{
    margin-bottom: 2vh;
}
.input_workshop{
    margin-bottom: 2vh;
}
.input_line{
    margin-bottom: 2vh;
}
</style>    