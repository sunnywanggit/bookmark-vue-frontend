<template>
    <Tree :data="data" :render="renderContent" class="demo-tree-render"></Tree>
</template>
<script>
    export default {
        data() {
            return {
                data: [
                    {
                        title: '我的收藏夹',
                        expand: true,
                        render: (h, {root, node, data}) => {
                            return h(
                                'span',
                                {style: {display: 'inline-block', width: '100%'}},
                                [
                                    h('span', [
                                        h('Icon', { props: { type: 'ios-folder-outline' }, style: { marginRight: '8px' } }),
                                        h('span', data.title)
                                    ]),
                                    h('span', { style: { display: 'inline-block', float: 'right', marginRight: '32px' } },
                                        [ h('Button', {
                                            props: Object.assign({}, this.buttonProps, { icon: 'ios-add', type: 'primary' }),
                                            style: { width: '64px' },
                                            on: { click: () => { this.append(node,data) } }
                                        }) ])
                                ])
                        },
                        children: [
                            {
                                title: 'child 1-1',
                                expand:false,
                                children: [
                                    { title: 'leaf 1-1-1', expand: false},
                                    { title: 'leaf 1-1-2', expand: false}
                                ]
                            }
                        ]
                    }
                ],
                buttonProps: { type: 'default', size: 'small', }
            }
        },
        methods: {
            renderContent(h, {root, node, data}) {
                console.log('render-content-data',root,node,data)
                return h(
                    'span', { style: { display: 'inline-block', width: '100%' } },
                    [
                    h('span', [
                        h('Icon', { props: { type: 'ios-paper-outline' }, style: { marginRight: '8px' } }),
                        h('span', data.title)
                    ]),
                    h('span', { style: { display: 'inline-block', float: 'right', marginRight: '32px' } },
                        [
                        h('Button', {
                            props: Object.assign({}, this.buttonProps, { icon: 'ios-add' }),
                            style: { marginRight: '8px' },
                            on: { click: () => { this.append(node,data) } }
                        }),
                        h('Button', {
                            props: Object.assign({}, this.buttonProps, { icon: 'ios-remove' }),
                            on: { click: () => { this.remove(root, node, data) } }
                        })
                    ])
                ])
            },
            append(node,data) {
                const children = data.children || []
                if(node.nodeKey >= 2){ this.$Message.warning('目录层级不能超过三级哦~'); return; }

                children.push({ title: 'appended node', expand: true })
                this.$set(data, 'children', children)
            },
            remove(root, node, data) {
                console.log('remove',root,node,data)
                const parentKey = root.find(el => el === node).parent
                const parent = root.find(el => el.nodeKey === parentKey).node
                const index = parent.children.indexOf(data)
                parent.children.splice(index, 1)
            }
        }
    }
</script>
<style>
    .demo-tree-render .ivu-tree-title {
        width: 100%;
        }
</style>
