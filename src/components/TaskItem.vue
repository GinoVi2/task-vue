<template>
    <v-card class="mb-3 bg-success">
        <v-card-title>
            {{ task.name }}
        </v-card-title>
        <v-card-subtitle>
            {{ isCompleted }}
        </v-card-subtitle>
        <v-card-actions class="d-flex justify-space-around">
            <v-btn
                :disabled="task.completed ? true : false"
                @click="$emit('complete-task', task)"
                class="bg-success"
                variant="outlined"
            >
                Completar
            </v-btn>
            <v-btn
                @click="$emit('delete-task', task)"
                class="bg-error"
                variant="outlined"
            >
                Borrar
            </v-btn>
        </v-card-actions>
    </v-card>
</template>
<script setup>
import { computed } from "vue";

const props = defineProps({
    task: Object,
});

const emits = defineEmits(["delete-task", "complete-task"]);

const isCompleted = computed(() =>
    props.task.completed ? "Tarea realizada" : "Tarea no realizada"
);
</script>
<style></style>
