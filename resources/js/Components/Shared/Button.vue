<template>
    <component :is="props.as" :class="buttonClass">
        <svg
            class="animate-spin h-5 w-5 absolute"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            v-if="props.loading"
        >
            <circle
                class="opacity-25"
                cx="12"
                cy="12"
                r="10"
                stroke="currentColor"
                stroke-width="4"
            ></circle>
            <path
                class="opacity-75"
                fill="currentColor"
                d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
            ></path>
        </svg>
        <component
            :is="props.leftIcon"
            :class="['w-5 h-5 mr-2', , props.loading && 'invisible']"
        ></component>
        <span :class="['mr-2', , props.loading && 'invisible']">
            <slot />
        </span>
        <component
            :is="props.rigthIcon"
            :class="['w-5 h-5 ml-2', , props.loading && 'invisible']"
        ></component>
    </component>
</template>
<script setup>
import { computed } from "vue";
import { cva } from "class-variance-authority";

const props = defineProps({
    leftIcon: Object,
    rigthIcon: Object,
    loading: Boolean,
    as: {
        type: [String, Object],
        default: "button",
    },
    intent: {
        type: String,
        validator: (val) =>
            ["primary", "secondary", "danger", "text"].includes(val),
        default: "secondary",
    },
});

const buttonClass = computed(() => {
    return cva(
        "inline-flex items-center justify-center text-sm rounded min-h-[32px] px-3 py-0.5 font-semibold ",
        {
            variants: {
                intent: {
                    primary: "bg-black text-white hover:bg-gray-800",
                    secondary: "bg-black/5  hover:bg-black/10 text-gray-700",
                    danger: "bg-red-600  hover:bg-red-500 text-white",
                    text: "  hover:bg-black/5 text-gray-700",
                },
            },
        }
    )({
        intent: props.intent,
    });
});
</script>
