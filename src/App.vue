<!-- this is an example -->
<template>
  <div class="page">
    <div class="nav">
      <multi-level-menu v-show="item.visible" v-for="item in catalogs" :key="item.id" :active="activeMenu" :data="item" :on-select="onSelectMenu"/>
    </div>
  </div>
</template>

<script>
  import TreeUtils from '@dadcici/tree-utils';
  import MultiLevelMenu from './components/multi-level-menu';

export default {
  components: {MultiLevelMenu},
   data() {
     return {
       tree: {},
       activeMenu: {},
       catalogs: [{
         id: 1,
         visible: true,
         name: 'name1',
         layer: 1,
         isOpen: false,
         children: [],
       }, {
         id: 2,
         visible: true,
         name: '8 level name2',
         layer: 1,
         isOpen: false,
         children: [{
           id: 21,
           visible: true,
           name: '8 level name2-1',
           layer: 2,
           isOpen: false,
           children: [{
             id: 211,
             visible: true,
             name: '8 level name2-1-1',
             layer: 3,
             isOpen: false,
             children: []
           }, {
             id: 212,
             visible: true,
             name: '8 level name2-1-2',
             layer: 3,
             isOpen: false,
             children: [ {
               id: 2121,
               visible: true,
               name: '8 level name2-1-2-1',
               layer: 4,
               isOpen: false,
               children: [{
                 id: 21211,
                 visible: true,
                 name: '8 level name2-1-2-1-1',
                 layer: 5,
                 isOpen: false,
                 children: [{
                   id: 212111,
                   visible: true,
                   name: '8 level name2-1-2-1-1-1',
                   layer: 6,
                   isOpen: false,
                   children: [{
                     id: 2121111,
                     visible: true,
                     name: '8 level name2-1-2-1-1-1-1',
                     layer: 7,
                     isOpen: false,
                     children: [{
                       id: 21211111,
                       visible: true,
                       name: '8 level name2-1-2-1-1-1-1-1',
                       layer: 8,
                       isOpen: false,
                       type: 'catalog',
                       children: []
                     }]
                   }]
                 }]
               }, {
                 id: 21212,
                 visible: true,
                 name: '8 level name2-1-2-1-2',
                 layer: 5,
                 isOpen: false,
                 children: []
               }]
             }]
           }, {
             id: 213,
             visible: true,
             name: 'name2-1-3',
             layer: 3,
             isOpen: false,
             children: []
           }]
         }, {
           id: 22,
           visible: true,
           name: 'name2-2',
           layer: 2,
           isOpen: false,
           children: []
         }, {
           id: 23,
           visible: true,
           name: 'name2-3',
           layer: 2,
           isOpen: false,
           children: []
         }],
       }, {
         id: 3,
         visible: true,
         name: 'name3',
         layer: 1,
         isOpen: false,
         children: [],
       }, {
         id: 4,
         visible: true,
         name: 'longest name，I am so long, yes, I am longest on the world.ah',
         layer: 1,
         isOpen: false,
         children: [{
           id: 41,
           visible: true,
           name: 'name4-1',
           layer: 2,
           isOpen: false,
           children: [{
             id: 411,
             visible: true,
             name: 'name4-1-1',
             layer: 3,
             isOpen: false,
             children: [],
           }],
         }],
       }, {
         id: 5,
         visible: true,
         name: 'name5',
         layer: 1,
         isOpen: false,
         children: [],
       }]
     }
   },
   methods: {
     onSelectMenu(menu) {
       this.activeMenu = menu;
       // 设置除自已外的路径上的节点的open状态
       let list = TreeUtils.getTreeChain(TreeUtils.tree2List(this.tree), menu.id, 'id');
       TreeUtils.traverse(this.tree, node => {
         if (node.id !== menu.id) {
           node.isOpen = list.indexOf(node.id) > -1;
         }
       });
       // 设置自已的状态
       menu.isOpen = !menu.isOpen;
       if (menu.type === 'catalog') {
       }
     },
   },
   created() {
     this.tree = { id: 0, root: 'root', children: this.catalogs };
     // 挂children和pid、isOpen
     TreeUtils.resetTree(this.tree, 'children', 0, 0);
   },
}
</script>

<style lang="scss">
  .page {
    .nav {
      border: 1px solid #eee;
      width: 250px;
      font-size: 14px;
      ul {
        list-style: none;
        padding: 0;
        margin: 0;
      }
    }
  }
</style>
