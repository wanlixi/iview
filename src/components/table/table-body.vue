<template>
    <table cellspacing="0" cellpadding="0" border="0" :style="style">
        <colgroup>
            <col v-for="column in columns" :width="setCellWidth(column, $index)">
        </colgroup>
        <tbody :class="[prefixCls + '-tbody']">
            <tr
                v-for="(index, row) in data"
                :class="[prefixCls + '-row', rowClsName(index), {[prefixCls + '-row-highlight']: cloneData[index] && cloneData[index]._isHighlight, [prefixCls + '-row-hover']: cloneData[index] && cloneData[index]._isHover}]"
                @mouseenter.stop="handleMouseIn(index)"
                @mouseleave.stop="handleMouseOut(index)"
                @click.stop="highlightCurrentRow(index)">
                <td v-for="column in columns" :class="alignCls(column)">
                    <Cell
                        :fixed="fixed"
                        :prefix-cls="prefixCls"
                        :row="row"
                        :column="column"
                        :index="index"
                        :checked="cloneData[index] && cloneData[index]._isChecked"></Cell>
                </td>
            </tr>
        </tbody>
    </table>
</template>
<script>
    import Cell from './cell.vue';
    import Mixin from './mixin';

    export default {
        mixins: [ Mixin ],
        components: { Cell },
        props: {
            prefixCls: String,
            style: Object,
            columns: Array,
            data: Array,
            cloneData: Array,
            fixed: Boolean
        },
        methods: {
            setCellWidth (column, index) {
                return this.$parent.setCellWidth(column, index);
            },
            rowClsName (index) {
                return this.$parent.rowClassName(this.data[index], index);
            },
            handleMouseIn (index) {
                this.$parent.handleMouseIn(index);
            },
            handleMouseOut (index) {
                this.$parent.handleMouseOut(index);
            },
            highlightCurrentRow (index) {
                this.$parent.highlightCurrentRow(index);
            }
        }
    }
</script>