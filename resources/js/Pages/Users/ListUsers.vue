<template>
    <app-layout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Usuarios en el sistema
            </h2>
            <div class="py-12">
                <div class="max-w-full mx-auto sm:px-6 lg:px-8">
                    <div class="overflow-hidden shadow-xl sm:rounded-lg">
                        <div
                            class="p-6 sm:px-20 bg-white border-b border-gray-200"
                        >
                            <div class="mt-8 flex flex-row m-2">
                                <p class="text-2xl ml-4 w-1/2">
                                    Usuarios activos en el sistema
                                </p>
                                <div class="w-1/2 flex justify-end">
                                    <jet-nav-link
                                        :href="route('admin.usuarios/create')"
                                    >
                                        <button
                                            class="border-green-700 border bg-white rounded mr-4 w-32 mb:w-42 p-1 hover:bg-aqua transition duration-500"
                                        >
                                            <div
                                                class="flex flex-row justify-center items-center"
                                            >
                                                <PlusIcon
                                                    class="block w-6 h-6 fill-gray-400"
                                                />
                                                <p class="font-bold">
                                                    Agregar Usuario
                                                </p>
                                            </div>
                                        </button>
                                    </jet-nav-link>
                                </div>
                            </div>
                            <div
                                class="overflow-auto rounded-lg shadow md:block"
                            >
                                <table class="w-full table-fixed">
                                    <thead
                                        class="bg-gray-50 border-b-2 border-gray-200"
                                    >
                                        <tr
                                            class="p-3 text-sm font-semibold tracking-wide text-left"
                                        >
                                            <th
                                                class="p-3 text-sm font-semibold tracking-wide text-left"
                                            >
                                                <div
                                                    class="flex content-center items-center"
                                                >
                                                    <UserIcon
                                                        class="w-4 h-4 mr-2"
                                                    />
                                                    Nombre de usuario
                                                </div>
                                            </th>
                                            <th class="px-6 pt-6 pb-4">
                                                <div
                                                    class="flex content-center items-center"
                                                >
                                                    <AtSymbolIcon
                                                        class="w-4 h-4 mr-2"
                                                    />
                                                    email
                                                </div>
                                            </th>
                                            <th class="px-6 pt-6 pb-4">
                                                <div
                                                    class="flex content-center items-center"
                                                >
                                                    <CalendarIcon
                                                        class="w-4 h-4 mr-2"
                                                    />
                                                    Departamento
                                                </div>
                                            </th>
                                            <th class="px-6 pt-6 pb-4">
                                                <div
                                                    class="flex content-center items-center"
                                                >
                                                    <BriefcaseIcon
                                                        class="w-4 h-4 mr-2"
                                                    />
                                                    Puesto
                                                </div>
                                            </th>
                                            <th class="px-6 pt-6 pb-4">
                                                <div
                                                    class="flex content-center items-center"
                                                >
                                                    <WrenchIcon
                                                        class="w-4 h-4 mr-2"
                                                    />
                                                    Acciones
                                                </div>
                                            </th>
                                        </tr>
                                    </thead>
                                    <tbody class="divide-y divide-gray-100">
                                        <tr
                                            v-for="user in users.data.usuarios"
                                            :key="user.data.id"
                                            class="hover:bg-gray-100 focus-within:bg-gray-100"
                                            :class="[
                                                user.data.attributes.activo == 0
                                                    ? 'text-gray-400'
                                                    : '',
                                            ]"
                                        >
                                            <td
                                                class="p-3 text-sm text-gray-700"
                                            >
                                                <p
                                                    class="font-bold text-blue-500 hover:underline"
                                                >
                                                    {{
                                                        user.data.attributes
                                                            .name
                                                    }}
                                                </p>
                                            </td>
                                            <td
                                                class="p-3 text-sm text-gray-700"
                                            >
                                                <p
                                                    class="pl-4 font-bold whitespace-pre-line"
                                                >
                                                    {{
                                                        user.data.attributes
                                                            .email
                                                    }}
                                                </p>
                                            </td>
                                            <td
                                                class="p-3 text-sm text-gray-700"
                                            >
                                                <span
                                                    class="p-1.5 text-xs font-medium uppercase tracking-wider text-blue-800 bg-blue-200 rounded-lg bg-opacity-50"
                                                >
                                                    {{
                                                        user.data.departamento
                                                            .data.attributes
                                                            .nombre
                                                    }}
                                                </span>
                                            </td>
                                            <td
                                                class="p-3 text-sm text-gray-700"
                                            >
                                                <span
                                                    class="p-1.5 text-xs font-medium uppercase tracking-wider text-green-800 bg-green-200 rounded-lg bg-opacity-50"
                                                >
                                                    {{
                                                        user.data.puesto.data
                                                            .attributes.nombre
                                                    }}
                                                </span>
                                            </td>
                                            <td
                                                class="p-3 text-sm text-gray-700"
                                            >
                                                <div
                                                    class="flex flex-row items-center text-gray-400 focus-within:text-gray-600"
                                                >
                                                    <ListBulletIcon
                                                        class="w-5 h-5 ml-3 pointer-events-none"
                                                    />
                                                    <jet-nav-link
                                                        :href="
                                                            route(
                                                                'admin.usuarios/edit',
                                                                {
                                                                    user: user
                                                                        .data
                                                                        .uuid,
                                                                }
                                                            )
                                                        "
                                                    >
                                                        <PencilIcon
                                                            class="w-5 h-5 ml-3 pointer-events-none"
                                                        />
                                                    </jet-nav-link>
                                                    <XMarkIcon
                                                        v-if="
                                                            user.data.attributes
                                                                .activo
                                                        "
                                                        class="w-5 h-5 ml-3 pointer-events-none"
                                                    />
                                                    <CheckBadgeIcon
                                                        v-else
                                                        class="w-5 h-5 ml-3 pointer-events-none"
                                                    />
                                                </div>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <div class="max-w-3xl mx-auto sm:px-6 lg:px-8 pt-4">
                                <pagination :meta="users.meta" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </template>
    </app-layout>
</template>

<script setup>
import { defineComponent, ref, computed, onMounted } from "vue";
import AppLayout from "@/Layouts/AppLayout.vue";
import JetNavLink from "@/Components/NavLink.vue";
import Pagination from "@/Components/Shared/Pagination.vue";
import {
    ListBulletIcon,
    PencilIcon,
    XMarkIcon,
    CheckBadgeIcon,
    HeartIcon,
    PlusIcon,
    AtSymbolIcon,
    CalendarIcon,
    UserIcon,
    BriefcaseIcon,
    WrenchIcon,
} from "@heroicons/vue/24/outline";

const props = defineProps({
    users: Object,
});
</script>
