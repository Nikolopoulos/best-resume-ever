<template>
  <div class="resume">
    <div class="banner">
      <div class="banner__fullname">{{ person.name.first }} {{ person.name.middle }} {{ person.name.last }}</div>
      <div class="banner__position">{{ person.position }}</div>
      <div v-if="person.birth" class="banner__location">{{ lang.born }} {{person.birth.year}} {{ lang.bornIn }} {{person.birth.location}}</div>
    </div>

    <div class="content">
      <div class="content__left">
        <div class="section">
          <div class="section-headline">
            {{ lang.about }}
          </div>

          <div class="section-content section-content--plain">
            {{ person.about }}
            <br/>
            <br/>
            {{ person.knowledge }}
          </div>
        </div>

        <div
          v-if="person.skills"
          class="section">
          <div class="section-headline">
            {{ lang.skills }}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(skill, index) in person.skills"
              class="grid-item"
              :key="index"
              :href="skill.url">
              <span class="squarred-grid-item">
                {{ skill.name }}
              </span>
            </a>
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            {{ lang.contact }}
          </div>

          <div class="section-content section-content--plain">
            <div class="section-link">
              <i class="section-link__icon material-icons">business</i>{{ person.contact.street }}, {{ person.contact.city }} 
            </div>

            <a
              class="section-link"
              :href="contactLinks.email">
              <i class="section-link__icon material-icons">mail</i>{{ person.contact.email }}
            </a>

            <div class="section-link">
              <i class="section-link__icon material-icons">phone</i>{{ person.contact.phone }}
            </div>

            <a
              v-if="person.contact.website"
              class="section-link"
              :href="person.contact.website">
              <i class="section-link__icon fa fa-globe"></i>{{ person.contact.website }}
            </a>

            <a
              v-if="person.contact.linkedin"
              class="section-link"
              :href="contactLinks.linkedin">
              <i class="section-link__icon fa fa-linkedin"></i>{{ person.contact.linkedin }}
            </a>

            <a
              v-if="person.contact.github"
              class="section-link"
              :href="contactLinks.github">
              <i class="section-link__icon fa fa-github"></i>{{ person.contact.github }}
            </a>

            <a
              v-if="person.contact.medium"
              class="section-link"
              :href="contactLinks.medium">
              <i class="section-link__icon fa fa-medium"></i>{{ person.contact.medium }}
            </a>
          </div>
        </div>
      </div>

      <div class="content__right">
        

        <div
          v-if="person.publications"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">book</i>{{ lang.publications }}
          </div>

          <div class="section-content">
            <a v-for="(publication, index) in person.publications" :key="index"
              class="section-content__item-grid"
              :href="publication.url">
              <span class="section-content__header"> {{ publication.name }} </span>
              <span class="section-content__subheader">{{ publication.issue }}</span>
            </a>
          </div>
        </div>

        <div
          v-if="person.certifications"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon fa fa-check"></i>{{lang.certifications}}
          </div>

          <div class="section-content">
            <a
              v-for="(certification, index) in person.certifications"
              class="section-content__item"
              :key="index"
              :href="certification.url">
              <span class="section-content__header"> {{ certification.name }} </span>
              <span class="section-content__text"> {{ certification.issuer }} </span>
            </a>
          </div>
        </div>




      </div>
    </div>

    <img class="picture"/>
  </div>
  
</template>


<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'custom2';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@accent-color: #34495E;
@banner-color: #42b883;
@banner-height: 120px;
@picture-size: 180px;
@picture-offset: 35px;
@base-padding: 30px;
@left-column-width: 240px;

a {
  color: inherit;
  cursor: pointer;
  text-decoration-line: none;

  &:visited {
    color: inherit;
  }
}

.resume {
  position: relative;
  font-family:'Roboto' !important;
  font-size: 0.9em;
}

.pictureASD {
  position: absolute;
  top: @banner-height - @picture-offset;
  left: @left-column-width + @base-padding * 2 - @picture-size / 2;
  height: @picture-size;
  width: @picture-size;
  border-radius: 50%;
  border: 5px solid @accent-color;
  content: url('../../resume/id.jpg');
  z-index: 2;
}

.picture {
  position: absolute;
  top: 0*0.1;
  left: @picture-size / 4;
  height: @picture-size;
  width: auto;
  /*border-radius: 50%;
  border: 5px solid @accent-color;*/
  content: url('../../resume/new_vc_pic.png');
  z-index: 2;
}

.banner {
  width: calc(100% - @base-padding * 2);
  height: @banner-height;
  padding: @base-padding;
  background-color: @banner-color;
  
  background-image: url('../../resume/banner.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  
  color: white;

  &__fullname {
    font-size: 32px;
    position: relative;
    top: @banner-height - @banner-height/2;
    text-align: right;
  }

  &__position {
    font-size: 16px;

    position: relative;
    top: @banner-height - @banner-height/2;
    text-align: right;
  }

  &__location {
    text-align: right;
    position: relative;
    top: @banner-height - @banner-height/2;
    font-size: 12px;
  }
}

.content {
  display: flex;
  width: 100%;
  height: 100%;

  &__left,
  &__right {
    height: 100%;
    padding: @base-padding;
  }

  &__left {
    width: @left-column-width;
    color: rgba(255, 255, 255, 0.59);
    background-color: @accent-color;

    .section-headline {
      color: white;
    }
  }

  &__right {
    flex: 1;
  }
}

.section {
  margin: 20px 0;
}

.section-link,
.section-headline {
  display: flex !important;
  align-items: center;
  color: @accent-color;
  display: inline-block;
  font-size: 1.2em;
  margin: 8px 0;

  &__icon {
    margin-right: 8px;
    font-size: 1.4em;
  }
}

.section-link {
  font-size: 1.1em;
  color: rgba(255, 255, 255, 0.59) !important;

  &__icon {
    color: white;
  }
}

.section-content {
  margin-top: 5px;
  padding-left: 32px;
  font-size: 14px;

  &__item {
    display: block;
    margin-bottom: 5px;
  }

  &__header {
    display: block;
    font-size: 1.1em;
    font-weight: 500;
  }

  &__subheader {
    display: block;
    font-weight: 400;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
    }
  }

  &__plain {
    display: inline;
    font-weight: 300;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
  }

  &--plain {
    padding: 0;
  }
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  margin-top: 5px;
  margin-bottom: 5px;
}

.grid-item {
  padding-right: 5px;
}

.squarred-grid-item {
  display: block;
  border: 1px solid white;
  color: white;
  margin-top: 5px;
  padding: 5px;
}
</style>
