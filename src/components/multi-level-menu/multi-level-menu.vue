<template>
  <ul class="multi-level-menu" :class="{ 'menu-co-active': active&&active.id===data.id&&data.layer!==1 }">
    <li class="menu-wrap" @click="onSelect(data)" >
      <div class="menu" :class="{
                              'main':data.layer===1,
                              'active': data.id===active.id&&data.children.length===0&&data.layer!==1,
                              'line': data.layer<=2,
                              'open': data.isOpen
                            }" :title="data.name">
        <div class="name" :style="{'padding-left': data.layer*10 + 'px' }">
          <span>{{data.name}}</span>
        </div>
        <div v-if="data.children.length>0&&data.layer!==1">
          <i class="icon iconfont fold-icon" v-if="data.isOpen" >&#xe615;</i>
          <i class="icon iconfont fold-icon" v-else >&#xe628;</i>
        </div>
      </div>
    </li>
    <MultiLevelMenu v-show="item.visible&&(item.layer<=alwaysOpenLayer||data.isOpen)"
                    v-for="item in data.children"
                   :key="item.id"
                   :active="active"
                   :always-open-layer="alwaysOpenLayer"
                   :data="item"
                   :on-select="onSelect">
    </MultiLevelMenu>
  </ul>
</template>

<script>
  export default {
    name: 'MultiLevelMenu',
    props: {
      data: {
        type: Object
      },
      active: {
        type: Object
      },
      alwaysOpenLayer: {
        type: Number,
        default: 2
      },
      onSelect: {
        type: Function
      }
    }
  };
</script>

<style scoped lang="scss">
  .multi-level-menu {
    &.menu-co-active {
      background-color: #f2f2f2!important;
    }
    .menu-wrap {
      .main {
        font-size: 15px;
        font-weight: bold;
        display: flex;
        padding-top: 40px!important;
        &:before {
          content: ' ';
          border-left: 3px solid rgb(38, 189, 204);
        }
        &:hover {
          background: none!important;
        }
      }
      .menu {
        padding: 12px 12px 12px 0;
        display: flex;
        .name {
          width: 220px;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;
        }
        .fold-icon {
          position: relative;
          color: #aaa;
        }
        &.line {
          border-bottom: 1px solid #eee;
        }
        &:hover {
          cursor: pointer;
          background-color: rgba(38, 189, 204, .1);
        }
        &.open {
          color: rgb(38, 189, 204);
          .fold-icon {
            color: rgb(38, 189, 204);
          }
        }
        &.active {
          color: #fff;
          background-color: rgb(38, 189, 204);
          .fold-icon {
            color: #fff;
          }
        }
      }
    }
  }
</style>
