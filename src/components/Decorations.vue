<template>
    <div class="uk-article">
        <h2 class="uk-article-title">{{this.title}}</h2>
        <input type="text" :value="$store.state.validate.decoration" class="absolute" style="z-index: -10" required />
        <div class="uk-child-width-1-3@m" uk-grid>
            <div v-for="item in $store.state.decorations" :key="item.id">

                <div class="uk-inline uk-light relative">
                    <input type="hidden" v-if="this.checks == 'true'" class="with-cursor" />
                    <label :for="'decoration' + item.id">
                        <img v-bind:src="item.image" width="1800" height="1200" alt="">
                    </label>
                    <input v-if="this.checks == 'true'" :data-price="item.price" @click="$store.dispatch('setDecorations')" class="decorationValue uk-checkbox absolute top left" type="checkbox" :name="'decoration' + item.id" :id="'decoration' + item.id" :value="item.name" />
                    <div class="uk-overlay uk-overlay-primary uk-position-bottom uk-flex uk-flex-middle uk-grid-small uk-grid-collapse" uk-grid>
                        <div class="uk-text-truncate uk-width-expand">{{item.name}}</div>
                        <div class="uk-width-auto" v-if="this.inventory == 'true'">
                            <span v-if="item.inventory >= 0" :class="{'uk-badge uk-margin-small-right': 1, ' uk-badge-warning': item.inventory < item.notify}">
                                <span>{{item.inventory}} / {{item.limit}}</span>
                            </span>
                            <span v-if="item.inventory < 0" class="uk-badge uk-badge-success">
                                Sin inventario
                            </span>
                        </div>
                        <div class="uk-width-auto">
                            <div v-if="this.inventory == 'false'" class="uk-badge">${{
                                Number(item.price).toLocaleString('en-US', {
                                    minimumFractionDigits: 2,
                                    maximumFractionDigits: 2
                                })
                            }} {{$store.state.currency}}
                            </div>
                            <div v-if="item.inventory >= 0 && this.inventory == 'true'" style="min-width: 4rem">
                                <progress class="uk-progress uk-margin-remove" :value="item.inventory" min="0" :max="item.limit"></progress>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ListDecorations',
  props: {
    title: String,
    checks: Boolean,
    inventory: Boolean
  }
}
</script>

<style>
.uk-list li .uk-badge + .uk-badge {
    margin-left: 5px;
}
</style>
