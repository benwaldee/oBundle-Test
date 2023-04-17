# oBundle Project Overview
* Preview code: **ljj55wklvj**

* Site link: [click me!]( https://benjamin-joseph-waldee.mybigcommerce.com/special-items/)
### Feature 1
-----------------------------------
For the first feature, I had to get acquainted with how the default BigCommerce codebase works. The html files I needed were located in `templates` folder and the corresponding js files were located in `assets/js` folder. I also needed to understand how the images are grabbed and displayed, and I soon learned about the handlebar helper `getImageSrcset`.

After I spent some time reading and understanding what I needed, I included some event handlers and logic in the `category.js` file, as well as corresponding HTML in the `responsive-image.html` file. Below are a couple examples of the code:

 -- `templates/components/common/responsive-img.html` (lines 41)
  ```
    data-src="{{getImageSrcset image use_default_sizes=true}}"
    data-hoverimage='{{getImageSrcset images.[1] img size (cdn default) use_default_sizes=true}}' {{#unless
  ```

  -- `assets/js/theme/category.js`(lines 38-48)
  ```
   onShowProductSecondImage(e) {
        const card = $(e.currentTarget).find(".card-image");
        const image = card.attr("data-hoverimage");
        card.attr("srcset", image);
    }

    onRemoveProductSecondImage(e) {
        const card = $(e.currentTarget).find(".card-image");
        const image = card.attr("data-src");
        card.attr("srcset", image);
    }
  ```
### Features 2 & 3
-----------------------------------
Features 2 & 3 I completed together, since the logic for the add and remove button is different but required similar work. Also, when features are tied together like this, I prefer to work on them in at minimum on the same day, and preferably in a single block of time (like I did with these).

These features were more challenging, since I had to figure out how the cart functions in the codebase so I could access and manipulate it. I ended up writing several different functions in the `category.js` file to access and edit the cart. I also added the corresponding html in the `category.html` file. Here are a couple examples of the code:

  -- `templates/pages/category.html` (lines 50-55)
  ```
    <div class="add-all-to-cart">
      <div class="d-flex">
        <input type="button" class="button button--primary" id="addAllToCart" value="Add All To Cart"/>
      </div>
    </div>
  ```

  --  `templates/pages/category.html` (lines 22-32)`
  ```
    <div class="cart-notification">
      <div class="add-notification">
        <i class="fas fa-check-circle"></i>
        Items were successfully added to the cart!
      </div>
    </div>
    <div class="clear-both"></div>
  ```

  -- `assets/js/theme/category.js` (line 166)
  ```
    $("#addAllToCart").on("click", this.onAddAllToCart.bind(this));
  ```
   -- `templates/pages/category.html` (lines 50-53)
  ```
    <input type="button" class="button button--danger" id="removeAllItems" value="Remove All Items"/>
  ```

  --- `templates/pages/category.html` (lines 27-30)
  ```
  <div class="remove-notification">
      <i class="fas fa-check-circle"></i>
      Items were successfully removed from the cart!
    </div>
  ```

  -- `assets/js/theme/category.js` (lines 165-167)
  ```
  this.onCheckCart();
  ...
  $("#removeAllItems").on("click", this.onRemoveAllItems.bind(this));
  ```


### Bonus
-----------------------------------
The bonus was fun and involved some similar work that I've done on personal projects - accessing specific user data for a personalized website experience. After some poking around and research, I learned that I could simply access a "customer" object. From there, I just found the right place in the html to include the information. Here is the code:

-- `templates/components/common/header.html` (lines 15-39)
  ```
    {{#if customer}}
      <header class="customer-details w-100">
          <div class="customer-about">
              <p class="customer-name">
                  <i class="fas fa-user"></i>
                  {{customer.name}}
              </p>
              <p class="customer-email">
                  <i class="fas fa-envelope-square"></i>
                  {{customer.email}}
              </p>
              <p class="customer-phone">
                  <i class="fas fa-phone"></i>
                  {{customer.phone}}
              </p>
              <p class="customer-messages">
                  <i class="fas fa-envelope"></i>
                  {{#if customer.num_new_messages}}
                      {{customer.num_new_messages}}
                  {{else}}
                      <span>0</span>
                  {{/if}}
              </p>
          </div>
      </header>
    {{/if}}
  ```
  

**NOTE** All styling was done using a custom `styles.scss` file that I added to the scss folder and then imported to `theme.scss`
