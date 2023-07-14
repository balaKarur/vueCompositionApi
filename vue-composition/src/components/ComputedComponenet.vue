<template>
    <h3>Computed Componenet</h3>
    <div>Employees Present {{isEmployExist}}</div>
    <div>Full Name is {{fullname}}</div>
</template>
<script setup>
import { computed, reactive ,ref} from "vue";

let employees = reactive([{"name":"Bala"}]);
let firstName = ref("Bala");
let lastName = ref("V");
const isEmployExist = computed(() => {
    return  employees.length >0 ? "Yes Computed" : "No";
});
const fullname = computed({
    get(){
        return firstName.value +" "+lastName.value;
    },
    set(newValue){
        [firstName.value , lastName.value] = newValue.split(" ")
    }
})
fullname.value = "Bala subramani"
</script>