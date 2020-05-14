<template>
  <div class="breadcrumsWrap" v-if="pathInfo.object">
    <a class="channel" :href="pathInfo.object.url">{{pathInfo.object.title}}</a>
    ->
    <a class="widget" :href="pathInfo.widget.url">{{pathInfo.widget.title}}</a>
    <template v-if="pathInfo.group">
      ->
      <span>
        {{pathInfo.group}}
      </span>
    </template>
    <template v-if="pathInfo.file">
      ->
      <span>
        {{pathInfo.file}}
      </span>
    </template>
  </div>
</template>

<script>
import { channelData } from '../../assets/js/constance'

function getWidget (data, paths) {
  const path = `/${paths[0]}/${paths[1]}/`;
  const path1 = `/${paths[0]}/${paths[1]}`;
  return data.widget.find(item => ((item.url === path) || (item.url === path1)) );
}

export default {
  name: 'Breadcrumbs',
  data() {
    return {
      pathInfo: {}
    }
  },
 mounted () {
    this.setBread()
  },
  watch: {
     '$route' (to, from) {
      if (to.path !== from.path) {
        this.setBread()
      }
    }
  },
  methods: {
    setBread(){
      const val = this.$page;
      const paths = val.relativePath.split('/');
      if(!paths) {
        return ;
      }
      const pathInfo = {}
      pathInfo.object = {
        title: channelData[paths[0]].title,
        url: `/channel/${paths[0]}/`
      };
      pathInfo.widget = getWidget(channelData[paths[0]], paths);
      if (paths.length > 3) {
        pathInfo.group = paths[2];
        pathInfo.file = val.title;
      }
      this.pathInfo = pathInfo;
    }
  }
}
</script>

<style lang="less" scoped>
.breadcrumsWrap{
  width: 100%;
  position: fixed;
  top: 5.435vw;
  padding: 15px 3vw;
  background: #fff;
}
</style>