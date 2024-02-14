<script setup lang="ts">
import { ref } from "@vue/reactivity";
import AfficheMaison from "@/components/AfficheMaison.vue";
import { FormKit } from "@formkit/vue";
import { supabase } from "@/supabase";
import Form from "@/components/Form.vue";

const maison = ref ({});

async function upsertMaison(dataForm: any, node: { setErrors: (arg0: any[]) => void; }) {
 const { data, error } = await supabase.from("Maison").upsert(dataForm).select();
 if (error) node.setErrors([error.message])
 else {
     console.log(data);
 }
}

</script>

<template>
    <div>
        <Form/>
    </div>
</template>