<template>
    <jet-form-section @submitted="updateTrabajoInformation">
        <template #title> Información del usuario </template>

        <template #description> Actualizar información del usuario </template>

        <template #form>
            <!-- Departamentos-->
            <div
                class="col-span-6 sm:col-span-4"
                v-if="puestos && puestos.length > 0"
            >
                <jet-label for="puesto" value="Departamentos" />
                <BaseListbox
                    :options="departamentos"
                    placeholder="Seleccione Departamentos de Trabajo"
                    v-model="formTrabajo.departamento_id"
                />
            </div>
            <!-- Puesto -->
            <div
                class="col-span-6 sm:col-span-4"
                v-if="puestos && puestos.length > 0"
            >
                <jet-label for="puesto" value="Puesto" />
                <BaseListbox
                    :options="puestos"
                    placeholder="Seleccione Puesto de Trabajo"
                    v-model="formTrabajo.puesto_id"
                />

                <jet-input-error
                    :message="formTrabajo.errors.puesto"
                    class="mt-2"
                />
            </div>
        </template>

        <template #actions>
            <jet-action-message
                :on="formTrabajo.recentlySuccessful"
                class="mr-3"
            >
                Guardar.
            </jet-action-message>

            <jet-button
                :class="{ 'opacity-25': formTrabajo.processing }"
                :disabled="formTrabajo.processing"
            >
                Guardar
            </jet-button>
        </template>
    </jet-form-section>
</template>

<script>
import JetButton from "@/Components/PrimaryButton.vue";
import JetFormSection from "@/Components/FormSection.vue";
import JetInputError from "@/Components/InputError.vue";
import JetLabel from "@/Components/InputLabel.vue";
import JetActionMessage from "@/Components/ActionMessage.vue";
import JetSecondaryButton from "@/Components/SecondaryButton.vue";
import BaseListbox from "@/Components/Shared/BaseListbox.vue";
import { useForm } from "@inertiajs/inertia-vue3";
import { ref } from "vue";
import {
    Listbox,
    ListboxButton,
    ListboxOptions,
    ListboxOption,
} from "@headlessui/vue";
import { CheckIcon, ChevronUpDownIcon } from "@heroicons/vue/24/solid";

export default {
    props: ["departamentos", "puestos", "user"],
    components: {
        JetActionMessage,
        JetButton,
        JetFormSection,
        JetInputError,
        JetLabel,
        JetSecondaryButton,
        Listbox,
        ListboxButton,
        ListboxOption,
        ListboxOptions,
        CheckIcon,
        ChevronUpDownIcon,
        BaseListbox,
    },

    setup(props) {
        const departamentoActual = ref(
            props.departamentos.find(
                (departamento) =>
                    departamento.id ===
                    props.user.data.attributes.departamento_id
            )
        );
        const puestoActual = ref(
            props.puestos.find(
                (puesto) => puesto.id === props.user.data.attributes.puesto_id
            )
        );
        const formTrabajo = useForm({
            departamento_id: departamentoActual.value.id,
            puesto_id: puestoActual.value.id,
        });
        function updateTrabajoInformation() {
            formTrabajo.put(
                route("admin.usuarios/updatedatostrabajo", {
                    user: props.user.data.uuid,
                })
            );
        }
        return {
            updateTrabajoInformation,
            formTrabajo,
            departamentoActual,
            puestoActual,
        };
    },
};
</script>
