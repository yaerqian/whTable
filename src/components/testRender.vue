<script>
export default {
    name: 'test-render',
    data(){
        return {
            // $index: '',
            // $row: {}
        }
    },
    props: {
        columns: Array, // 表格列配置
        size: {
            type: String,
            default: 'mini'
        },
        data: Array, // 表格分页数据
    },
    render(createElement){
        return createElement(
            'div',
            {},
            [
                createElement(
                    'el-table',
                    {
                        props: {
                            data: this.data,
                            border: true,
                            align: 'center',
                            size: this.size,
                            style: 'width: 100%'
                        },
                    },
                    this.columns.map((item, index) => {
                        return createElement(
                            'el-table-column',
                            {
                                props:{
                                    label: item.label,
                                    prop: item.prop,
                                    align: 'center',
                                },
                                scopedSlots: {
                                    default: (scope) => {
                                        if(item.templateInfo){
                                            return createElement(
                                                'div',
                                                {},
                                                item.templateInfo.classify.map((v, i, arr) => {
                                                    if(v === 'el-button'){
                                                        return createElement(
                                                            v,
                                                            {
                                                                props:{
                                                                    type: item.templateInfo.type[i]?item.templateInfo.type[i]:'primary',
                                                                    size: this.size,
                                                                    disabled: item.templateInfo.disabled[i]?eval(item.templateInfo.disabled[i]):false
                                                                },
                                                                domProps: {
                                                                    innerHTML: item.templateInfo.content[i]
                                                                },
                                                                on: {
                                                                    click: (e) => {
                                                                        this.$emit(item.templateInfo.event[i], {
                                                                            row: scope.row,
                                                                            index: scope.$index
                                                                        })
                                                                    }
                                                                }
                                                            }
                                                        )
                                                    }else if(v === 'el-input'){
                                                        return createElement(
                                                            v,
                                                            {
                                                                props: {
                                                                    size: this.size,
                                                                    clearable: true,
                                                                    value: scope.row[item.prop],
                                                                    disabled: item.templateInfo.disabled[i]?eval(item.templateInfo.disabled[i]):false
                                                                },
                                                                on: {
                                                                    input: (value)=> {
                                                                        scope.row[item.prop] = value
                                                                    }
                                                                }
                                                                
                                                            }
                                                        )
                                                    }else if(v === 'el-select'){
                                                        return createElement(
                                                            v,
                                                            {
                                                                props: {
                                                                    size: this.size,
                                                                    value: scope.row[item.prop],
                                                                    clearable: true,
                                                                },
                                                                on: {
                                                                    change: (value) => {
                                                                        scope.row[item.prop] = value
                                                                    }
                                                                }
                                                            },
                                                            [
                                                                item.templateInfo.option[i].map((v, i, arr) => {
                                                                    return createElement(
                                                                        'el-option',
                                                                        {
                                                                            props:{
                                                                                key: arr[i].id,
                                                                                label: arr[i].label,
                                                                                value: arr[i].value
                                                                            }
                                                                        },
                                                                        []
                                                                    )
                                                                })
                                                            ]
                                                        )
                                                    }
                                                })
                                            )
                                        }else{
                                            return createElement('span', {domProps:{
                                                innerHTML: scope.row[item.prop]
                                            }})
                                        }
                                    }
                                },
                            },
                        )
                    })
                )
            ]
        )
    },
    methods: {
        
    }
}
</script>
