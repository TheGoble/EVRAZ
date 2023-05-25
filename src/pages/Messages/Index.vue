<template>
    <q-page>
        <div class="q-pa-md">
        <div>
            <q-btn class="button" color="secondary" @click="showWindow">Добавить сообщение</q-btn>
            <q-dialog v-model="showDialog">
            <q-card>
                <q-card-section>
                   Добавьте сообщение 
                </q-card-section>
                <q-card-section>
                    <q-input class="input_subject" standout="bg-secondary text-white" v-model="message.subject" label="Тема сообщения" />
                    <q-input class="input_body" standout="bg-secondary text-white" v-model="message.body" label="Тело сообщения" />
                    <q-select
                        filled
                        v-model="message.sensor"
                        multiple
                        :options="options"
                        option-label="sensorName"
                        label="Датчик"
                        style="width: 250px"
                        standout="bg-secondary"
                    />
                </q-card-section>
                <q-card-actions>
                <q-btn color="secondary" label="Закрыть" @click="closeWindow" />
                <q-btn class="button_add" color="secondary" label="Добавить" @click="addMessage"></q-btn>
                </q-card-actions>
            </q-card>
            </q-dialog>
        </div>
        <q-table
            title="Шаблон сообщений"
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
        showDialog: false,
        data: [],
        message: {
            subject: '',
            body: '',
            sensor: null,
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
            { name: 'Subject', align: 'center', label: 'Тема сообщения', field: 'subject'},
            { name: 'Body', label: 'Тело сообщения', field: 'body'},
            { name: 'sensor', label: 'Датчик', field: 'sensor' },
        ],
        options: [
            {
                sensorName: 'Датчик 1',
            },
            {
                sensorName: 'Датчик 2',
            }
        ],
    };
    },
    methods: {
        showWindow() {
        this.showDialog = true;
        },
        closeWindow() {
        this.showDialog = false;
        this.message.subject = '';
        this.message.body = '';
        this.message.sensor = null;
        },
        addMessage() {
            this.data.push({
                name: this.data.length + 1,
                ...this.message,
                sensor: this.generateSensors(this.message.sensor),
            })
            
            this.closeWindow();
        },
        generateSensors(sensors) {
            let sensorsList = ''
            for (let i = 0; i < sensors.length; i++) {
                if (i === sensors.length - 1) {
                    sensorsList += `${sensors[i].sensorName}`
                }
                else {
                    sensorsList += `${sensors[i].sensorName}; `
                }
                
            }
            return sensorsList
        }
    },
}
    

</script>

<style>
.button{
    margin-top: 3vh;
    margin-bottom: 5vh;
}
.input_subject{
    margin-bottom: 2vh;
}
.input_body{
    margin-bottom: 2vh;
}
</style>