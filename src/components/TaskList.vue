<template>
    <v-container fluid>
        <v-row>
            <v-col cols="12" md="4">
                <v-card>
                    <v-card-item>
                        <v-card-title> Agrega una nueva tarea </v-card-title>
                    </v-card-item>
                    <v-card-text>
                        <v-text-field
                            hide-details
                            v-model="newTask"
                            label="Tarea"
                        ></v-text-field>
                    </v-card-text>
                    <v-card-text class="d-flex justify-space-between">
                        <v-btn class="bg-success" @click="addTask">
                            Añadir
                        </v-btn>
                    </v-card-text>
                    <v-card-text>
                        <v-radio-group v-model="filter">
                            <v-radio
                                value="completed"
                                label="Completadas"
                                hide-details
                            ></v-radio>
                            <v-radio
                                value="pending"
                                label="Sin completar"
                                hide-details
                            ></v-radio>
                        </v-radio-group>
                    </v-card-text>
                </v-card>
            </v-col>
            <v-col cols="12" md="8">
                <template v-for="task of filteredList">
                    <TaskItem
                        @delete-task="deleteTask"
                        @complete-task="completeTask"
                        :task="task"
                    />
                </template>
            </v-col>
        </v-row>
    </v-container>
</template>
<script setup>
import { ref, computed } from "vue";
import TaskItem from "../components/TaskItem.vue";

const taskList = ref([
    {
        id: 1,
        name: "Tarea 1",
        completed: false,
    },
    {
        id: 2,
        name: "Tarea 2",
        completed: true,
    },
    {
        id: 3,
        name: "Tarea 3",
        completed: false,
    },
    {
        id: 4,
        name: "Tarea 4",
        completed: false,
    },
    {
        id: 5,
        name: "Tarea 5",
        completed: false,
    },
    {
        id: 6,
        name: "Tarea 6",
        completed: false,
    },
]);

const filteredList = computed(() => {
    if (filter.value == "completed") {
        return taskList.value.filter((task) => task.completed == true);
    } else if (filter.value == "pending") {
        return taskList.value.filter((task) => task.completed == false);
    }
    return taskList.value;
});

const newTask = ref("");

const filter = ref("");

const addTask = () => {
    if (newTask.value == "") return;

    //Obtener el ultimo id de la lista de tarea
    taskList.value.push({ id: 7, name: newTask.value, completed: false });
};

const completeTask = (tarea) => {
    taskList.value.forEach((task) => {
        if (task.id == tarea.id) {
            task.completed = true;
        }
    });
};

const deleteTask = (tarea) => {
    taskList.value = taskList.value.filter((task) => task.id != tarea.id);
};
</script>
<style></style>
