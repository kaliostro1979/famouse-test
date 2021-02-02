<template>
  <div id="main">
    <header class="header">
      <div class="container">
        <div class="row">
          <div class="col-7">
            <div class="top">
              <div class="top__logo">
                <a href="#"><img :src="'.' + '/images/' + logo" alt="logo"></a>
              </div>
              <div class="nav">
                <ul class="nav__list">
                  <li class="nav__list-item"
                      v-for="navItem in navItems" :key="navItem"
                  >
                    <a href="#">{{ navItem }}</a>
                  </li>
                </ul>
              </div>
            </div>
          </div>
          <div class="col-5">
            <div class="search">
              <div class="search__input">
                <input class="search__input" type="text" :placeholder="searchInputPlaceHolder">
              </div>
              <div class="search__btn">
                <button class="item-btn">{{ searchBtnText }}</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </header>
    <section class="store">
      <div class="store__main">
        <div class="container">
          <div class="row">
            <div class="col-12">
              <h1 class="store__main-title">{{ title }}</h1>
            </div>
          </div>
          <div class="row">
            <div class="col-3" v-for="(card, id) in cardItem" :key="card.name">
              <div :class="{
                            'store__main-cards-item': true,
                            'store__main-cards-item-disabled': card.available === false
                        }">
                <div class="store__main-cards-item-img" :style="{'background-image': card.image}">
                </div>
                <div class="store__main-cards-item-info-wrapper">
                  <div class="store__main-cards-item-title">
                    <h2>{{ card.id }}{{ card.title }}</h2>
                  </div>
                  <div class="store__main-cards-text">
                    <p>Продана на аукционе</p>
                  </div>
                  <div class="row">
                    <div class="store__main-cards-item-price">
                      <p class="old-price">{{ card.price }}</p>
                      <p :class="{
                                        'new-price': true,
                                        'new-price-show': card.offerPrice !== 0
                                    }">{{ card.offerPrice }}</p>
                    </div>
                    <div class="store__main-cards-item-btn">
                      <div
                          :class="{
                                            'item-btn-loader':true,
                                            'item-btn-loader-show':card.loading === true
                                         }"
                      >
                        <img :src="'.' + '/images/icons/' + card.loaderImg">
                      </div>
                      <button
                          :class="{
                                            'item-btn':true,
                                            'buy':card.status === true,
                                            'sold':card.status === false
                                         }"
                          @click="buyHandler(id)"
                          :disabled='card.isDisabled'
                      >{{ card.loading ? '' : card.btnText }}
                      </button>
                      <div class="sold-icon">
                        <img :src="card.btnIcon" alt="">
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <footer class="footer">
      <div class="container">
        <div class="row">
          <div class="col-7">
            <div class="top">
              <div class="top__logo">
                <a href="#"><img :src="'.' + '/images/' + logo" alt="logo"></a>
              </div>
              <div class="nav">
                <ul class="nav__list">
                  <li class="nav__list-item"
                      v-for="navItem in navItems"
                      :key="navItem"
                  >
                    <a href="#">{{ navItem }}</a>
                  </li>
                </ul>
              </div>
            </div>
          </div>
          <div class="col-5">
            <div class="contacts">
              <ul class="contacts__list">
                <li class="contacts__list-item" v-for="contactsItem in contacts" :key="contactsItem.name">
                  <div class="contacts__list-item-icon">
                    <img :src="'.' + '/images/icons/' + contactsItem.icon" alt="icon">
                  </div>
                  <p class="contacts__list-item-text">{{ contactsItem.text }}</p>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {},
  data: () => {
    return {
      logo: 'logo.png',
      navItems: [
        'Каталог',
        'Доставка',
        'Оплата',
        'Контакты',
        'О галерее'
      ],
      searchBtnText: 'Найти',
      searchInputPlaceHolder: 'Поиск по названию картины',
      title: 'Картины эпохи Возрождения',
      cardItem: [
        {
          id: 1,
          image: 'url("./images/img-1.png")',
          title: '«Рождение Венеры» Сандро Боттичелли',
          price: '2 000 000$',
          offerPrice: '1 000 000$',
          btnText: 'Купить',
          status: true,
          loading: false,
          loaderImg: 'loader.svg',
          isDisabled: false,
          available: true,
          btnIcon: './images/icons/btn-mark.svg'
        },
        {
          id: 2,
          image: 'url("./images/img-2.png")',
          title: '«Тайная вечеря»  Леонардо да Винчи',
          price: '3 000 000$',
          offerPrice: '1 500 000$',
          btnText: 'Купить',
          status: true,
          loading: false,
          loaderImg: 'loader.svg',
          isDisabled: false,
          available: true,
          btnIcon: './images/icons/btn-mark.svg'
        },
        {
          id: 3,
          image: 'url("./images/img-3.png")',
          title: '«Сотворение Адама» Микеланджело',
          price: '5 000 000$',
          offerPrice: '3 000 000$',
          btnText: 'Купить',
          status: true,
          loading: false,
          loaderImg: 'loader.svg',
          isDisabled: false,
          available: true,
          btnIcon: './images/icons/btn-mark.svg'
        },
        {
          id: 4,
          image: 'url("./images/img-4.png")',
          title: '«Урок анатомии»  Рембрандт',
          price: ' 6 000 000$',
          offerPrice: 0,
          btnText: 'Купить',
          status: true,
          loading: false,
          loaderImg: 'loader.svg',
          isDisabled: false,
          available: false,
          btnIcon: './images/icons/btn-mark.svg'
        },
      ],
      contacts: [
        {
          name: 'Телефон',
          icon: 'tel.svg',
          text: '+7 (495) 555-55-55'
        },
        {
          name: 'Адрес',
          icon: 'address.svg',
          text: 'г. Москва, ул. Расплетина, 24'
        }
      ]
    }
  },
  mounted() {
    if (localStorage.getItem('cardItem')) {
      try {
        this.cardItem = JSON.parse(localStorage.getItem('cardItem'));

      } catch (e) {
        localStorage.removeItem('cardItem');
      }
    }
  },
  methods: {
    async buyHandler(id) {
      try {
        this.cardItem[id].loading = true
        await fetch('https://jsonplaceholder.typicode.com/posts/1')
            .then((res) => {
              return res.json()
            })
            .then(() => {
              this.cardItem[id].loading = false
              this.cardItem[id].btnText = 'В корзине'
              this.cardItem[id].status = false
              this.cardItem[id].isDisabled = true
              this.saveBtnText();
            })
      } catch (error) {
        this.cardItem[id].loading = false
        this.cardItem[id].btnText = 'Купить'
        this.cardItem[id].status = true
      }
    },
    saveBtnText() {
      const parsedCardItem = JSON.stringify(this.cardItem);
      localStorage.setItem('cardItem', parsedCardItem);
    }
  }
}
</script>


<style lang="scss">
@import "../assets/scss/grid.scss";
@import "../assets/css/fonts.css";
@import "../assets/scss/global.scss";
@import "../assets/scss/style.scss";
</style>
