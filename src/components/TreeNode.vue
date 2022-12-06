<template>
    <label :style="nodeMargin" show class="d-flex justify-content-between mb-1">
        {{ node.label }}
        <span class="fas fa-angle-right"></span>
    </label>    
    <div v-if="hasChildren">
      <TreeNode
        v-for="child in node.children"
        :key="child.id"
        :node="child"
        :spacing="(spacing + 10)"
      />
    </div>
</template>

<script>
    export default {
        name: 'TreeNode',
        props: {
            node: {
                type: Object,
                required: true
            },
            spacing: {
                type: Number,
                default: 0
            }
        },
        computed: {
            nodeMargin() {
                return {
                    'margin-left': `${this.spacing}px`
                }
            },
            hasChildren() {
                const {children} = this.node
                return children && children.length > 0
            }
        }
    }
</script>

<style scoped>

</style>



