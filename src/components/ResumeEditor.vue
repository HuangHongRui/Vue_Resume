<template>
  <div id="resumeEditor">
    <nav>
      <ol>
        <li v-for="(item,index) in resume.config"
          v-bind:class="{ active: item.field === selected }"
          v-on:click="selected = item.field"
          >
          <svg class="icon">
            <use v-bind:xlink:href="`#icon-${item.icon}`"></use>
          </svg>
        </li>
      </ol>
    </nav>
    <ol class="panels">
      <li v-for="item in resume.config" v-show="item.field === selected">
        <div v-if="resume[item.field] instanceof Array">
          <div class="subitem" v-for="subitem in resume[item.field]">
            <div class="resumeField" v-for="(value, key) in subitem">
              <label>{{key}}</label>
              <input type="text" v-bind:value="value">
            </div>
            <hr>
          </div>
        </div>
        <div v-else class="resumeField" v-for="(value, key) in resume[item.field]">
          <label> {{key}} </label>
          <input type="text" v-model="resume[item.field][key]">
        </div>
      </li>
    </ol>
  </div>
</template>


<script>
  export default {
    name: 'ResumeEditor',
    data() {
      return {
        selected: 'profile',
        resume: {
          config: [
            {field: 'profile', icon: 'id'},
            { field: 'work history', icon: 'work'  },
            { field: 'education', icon: 'book'  },
            { field: 'projects', icon: 'heart'  },
            { field: 'awards', icon: 'cup'  },
            { field: 'contacts', icon: 'phone'  },
          ],
          profile: { name: '', city: '', title: '' },
          'work history': [
            { company: 'AL', content: '我的第二份工作是'  },
            { company: 'TX', content: '我的第一份工作是'  },
          ],
          education: [
            { school: 'AL', content: '文字'  },
            { school: 'TX', content: '文字'  },
          ],
          projects: [
            { name: 'project A', content: '文字'  },
            { name: 'project B', content: '文字'  },
          ],
          awards: [
            { name: 'awards A', content: '文字'  },
            { name: 'awards B', content: '文字'  },
          ],
          contacts: [
            { contact: 'Phone', content: '1000000000'  },
            { contact: 'QQ', content: '2000000000'  },
          ],
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  #resumeEditor {
    background: #fff;
    box-shadow: 0 1px 3px 0 rgba(0,0,0,0.25);
    display: flex;
    flex-direction: row;
    overflow: auto;
    > .panels {
      flex-grow: 1;
      > li {
        padding: 24px;
      }
      .resumeField {
        > label {
          display: block;
        }
        input[type=text] {
          margin: 16px 0;
          border: 1px solid #ddd;
          box-shadow: inset 0 1px 3px 0 rgba(0,0,0,0.3);
          width: 100%;
          height: 32px;
          padding: 0 8px;
        }
      }
      hr {
        border: none;
        border-top: 1px solid #ddd;
        margin: 24px 0;
        overflow: visible;
      }
    }
    
    > ol {
      list-style: none;
    }
    > nav {
      width: 80px ;
      background: #000;
      color: #fff;
      > ol {
        > li {
          height: 48px;
          display: flex;
          justify-content: center;
          align-items: center;
          margin-top: 16px;
          margin-bottom: 16px;
          &.active {
            background-color: #fff;
            color: #000;
          } 
          > svg.icon {
            width: 24px;
            height: 24px;
          }

        }
      }
    }
  }
</style>
