<template>
    <div
        :class="[
            'item-task d-flex align-items-start border-bottom pt-3 pb-4',
            isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12'
        ]"
    >
        <div
            :class="[
                'd-flex flex-column'
            ]"
        >
            <div class="name-university mb-1">
                {{ university.name }}
            </div>
            <div class="review-university">
                {{ university.review }}
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        university: {
            type: Object,
            default() {
                return {}
            }
        }
    },
    isGrid: {
        type: Boolean,
        required: true,
        default: false
    },
    computed: {
            localUniversity: {
                get() {
                    return this.university
                },
                set(newValue) {
                    this.$emit('update:university', newValue)
                },
            },
        }
}
</script>