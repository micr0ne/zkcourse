<script setup>
import { data } from './data/member.data.ts'
import { ref, toRaw } from 'vue';
import { useData } from 'vitepress'

const members = ref(data.data) 
function shorten(name, maxLen = 10, ellipsis='...' ) {
  return name.length <= maxLen? name : (name.slice(0, maxLen) + ellipsis);
}

const { site } = useData();
const pattern = toRaw(site.value.themeConfig?.editLink)?.pattern;
const link = pattern ? pattern.replace(":path", "data/member.data.ts") : undefined;
</script>

# 学员列表

<span v-if="link">
请通过<a :href="link" target="_blank">此链接</a>修改个人资料。
</span>

<table>
  <tr>
    <th>microne</th>
    <th>硕士在读</th>
    <th>对web3的zkp领域较为感兴趣，希望能系统学习zkp技术和理论。以后也想在zkp领域找一些工作机会</th>
  </tr>
  <tr v-for="m in members">
    <td>{{ shorten(m.name) }}</td>
    <td>{{ shorten(m.job, 20) }}</td>
    <td>{{ m.intro }}</td>
  </tr>
</table>
