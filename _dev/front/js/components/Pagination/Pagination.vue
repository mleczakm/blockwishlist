<!--**
 * 2007-2020 PrestaShop and Contributors
 *
 * NOTICE OF LICENSE
 *
 * This source file is subject to the Academic Free License 3.0 (AFL-3.0)
 * that is bundled with this package in the file LICENSE.txt.
 * It is also available through the world-wide-web at this URL:
 * https://opensource.org/licenses/AFL-3.0
 * If you did not receive a copy of the license and are unable to
 * obtain it through the world-wide-web, please send an email
 * to license@prestashop.com so we can send you a copy immediately.
 *
 * @author    PrestaShop SA <contact@prestashop.com>
 * @copyright 2007-2020 PrestaShop SA and Contributors
 * @license   https://opensource.org/licenses/AFL-3.0 Academic Free License 3.0 (AFL-3.0)
 * International Registered Trademark & Property of PrestaShop SA
 *-->
<script>
  import EventBus from '@components/EventBus';

  /**
   * Dumb component to display the list of Wishlist on a page
   */
  export default {
    name: 'Pagination',
    data() {
      return {
        total: null,
        minShown: null,
        maxShown: null,
        pageNumber: 0,
        pages: [],
        currentPage: null,
        display: false,
      };
    },
    methods: {
      paginate(page) {
        EventBus.$emit('updatePagination', {
          page,
        });

        this.currentPage = page;
      },
    },
    mounted() {
      EventBus.$on('paginate', (payload) => {
        this.total = payload.detail.total;
        this.minShown = payload.detail.minShown;
        this.maxShown = payload.detail.maxShown;
        this.pageNumber = payload.detail.pageNumber;
        this.currentPage = payload.detail.currentPage;
        this.pages = payload.detail.pages;
        this.display = payload.detail.display;
      });
    },
  };
</script>

<style lang="scss" type="text/scss">
  @import '@scss/_variables';

  .wishlist {
    &-pagination {
      .previous {
        margin-right: 1.875rem;
      }

      .js-search-link {
        cursor: pointer;

        &:not([href]):not([tabindex]):hover {
          color: $blue;
        }

        &.disabled {
          cursor: inherit;

          &:hover {
            color: $blue;
          }
        }
      }
    }
  }
</style>
