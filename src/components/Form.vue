<script setup lang="ts">
import { ref } from "@vue/reactivity";
import AfficheMaison from "@/components/AfficheMaison.vue";
import { FormKit } from "@formkit/vue";
import { supabase } from "@/supabase";

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
        <div class="p-2">
            <h2 class="text-2xl">
                Résultat (Prévisualisation)
            </h2>
            <AfficheMaison v-bind="maison" />
        </div>
        <div class="p-2">
            <FormKit @submit="upsertMaison"  type="form" v-model="maison">
                <FormKit name="nomMaison" label="nom de la maison" />
                <FormKit name="adresse" label="adresse" />
                <FormKit name="prix" type="number" label="prix" />
                <FormKit name="favori" type="checkbox" label="mettre en valeur" />
                <FormKit name="nbrChambres" type="number" label="nombre de chambres" />
                <FormKit name="nbrSDB" type="number" label="nombre de salle de bain" />
                <FormKit name="surface" label="surface" />
                <FormKit name="image" label="image" />

            </FormKit>
        </div>
    </div>
</template>