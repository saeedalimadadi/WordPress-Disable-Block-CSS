# WordPress Disable Block CSS

This code snippet provides a solution to **remove the default CSS files associated with WordPress blocks and WooCommerce blocks**. By default, WordPress loads `wp-block-library.css` and `wp-block-library-theme.css` for the Gutenberg editor blocks, and WooCommerce loads `wc-blocks-style.css` if block-based elements are present. If you are using a page builder, a custom theme, or simply don't use Gutenberg blocks on your frontend, dequeueing these stylesheets can help improve page load times and reduce unnecessary CSS.

## Why disable Block CSS?

* **Performance Optimization:** Reduces the number of HTTP requests and the total size of CSS loaded on your website, leading to faster page load times.
* **Cleaner Code:** Removes CSS that might be redundant if your theme or page builder already provides its own styling for common elements or if you don't use blocks.
* **Avoid Conflicts:** Helps prevent potential styling conflicts between the default block CSS and your theme's or page builder's CSS.
* **Full Control:** Gives you complete control over what CSS is loaded on your frontend.

## Features

* **Dequeues `wp-block-library.css`:** Removes the core Gutenberg block styling.
* **Dequeues `wp-block-library-theme.css`:** Removes the default theme-specific Gutenberg block styling.
* **Dequeues `wc-blocks-style.css`:** Removes the CSS for WooCommerce blocks (e.g., product grids, cart blocks).
* Applies on the frontend of your website.

## Installation

There are two primary methods to implement this code:

### Method 1: As a Standalone Plugin (Recommended)

Creating a small, dedicated plugin is the most robust way to add this functionality. It ensures your modification remains active regardless of theme changes.

1.  Create a new folder named `wp-no-block-css` inside your WordPress site's `wp-content/plugins/` directory.
2.  Inside this new folder, create a file named `wp-no-block-css.php`.
3.  Copy and paste the following code into `wp-no-block-css.php`:

    ```php
    <?php
    /**
     * Plugin Name: WordPress Disable Block CSS
     * Description: Removes default Gutenberg and WooCommerce block CSS from the frontend for performance optimization.
     * Version: 1.0
     * Author: Your Name (Optional)
     * License: GPL-2.0-or-later
     */

    if ( ! defined( 'ABSPATH' ) ) {
        exit; // Exit if accessed directly.
    }

    /**
     * Dequeues default WordPress and WooCommerce block CSS files.
     */
    function mehdiamdev_remove_wp_block_library_css(){
        wp_dequeue_style( 'wp-block-library' );
        wp_dequeue_style( 'wp-block-library-theme' );
        wp_dequeue_style( 'wc-blocks-style' ); // Remove WooCommerce block CSS
    }
    add_action( 'wp_enqueue_scripts', 'mehdiamdev_remove_wp_block_library_css', 100 );
    ?>
    ```

4.  Go to your WordPress admin dashboard, navigate to **"Plugins"**, and **activate** the "WordPress Disable Block CSS" plugin.

### Method 2: Adding to your Theme's functions.php File

You can add this code directly to your active theme's `functions.php` file. **Before doing so, it's highly recommended to back up your `functions.php` file.**

1.  Navigate to `wp-content/themes/YourThemeName/` (replace `YourThemeName` with the actual name of your active theme).
2.  Open the `functions.php` file.
3.  Add the following code to the end of the file (before the closing `?>` tag, if one exists):

    ```php
    /**
     * Dequeues default WordPress and WooCommerce block CSS files.
     */
    function mehdiamdev_remove_wp_block_library_css(){
        wp_dequeue_style( 'wp-block-library' );
        wp_dequeue_style( 'wp-block-library-theme' );
        wp_dequeue_style( 'wc-blocks-style' ); // Remove WooCommerce block CSS
    }
    add_action( 'wp_enqueue_scripts', 'mehdiamdev_remove_wp_block_library_css', 100 );
    ```

## Important Considerations

* **Visual Impact:** **Crucially, if you use Gutenberg blocks on your frontend pages or posts, removing these CSS files will likely break their styling.** Ensure your theme or page builder provides the necessary CSS for any blocks you use, or avoid using blocks on the frontend entirely.
* **WooCommerce Blocks:** If you use the newer WooCommerce blocks (e.g., in your cart, checkout, or shop pages), dequeueing `wc-blocks-style` will affect their appearance. Test thoroughly.
* **Testing:** Always test your site thoroughly after implementing this code to ensure no visual or functional issues arise due to missing CSS.

## Contributing

Contributions are welcome! If you have suggestions or improvements for this code, feel free to open a "Pull Request" or report an "Issue."

## License

This project is licensed under the GPL-2.0-or-later License.

---

# غیرفعال‌سازی CSS بلوک‌های وردپرس

این قطعه کد راه حلی برای **حذف فایل‌های CSS پیش‌فرض مرتبط با بلوک‌های وردپرس و بلوک‌های ووکامرس** ارائه می‌دهد. به طور پیش‌فرض، وردپرس فایل‌های `wp-block-library.css` و `wp-block-library-theme.css` را برای بلوک‌های ویرایشگر گوتنبرگ بارگذاری می‌کند و ووکامرس نیز `wc-blocks-style.css` را در صورت وجود عناصر مبتنی بر بلوک بارگذاری می‌کند. اگر از یک صفحه ساز، یک قالب سفارشی استفاده می‌کنید یا به سادگی از بلوک‌های گوتنبرگ در فرانت‌اند سایت خود استفاده نمی‌کنید، حذف این برگه‌های استایل می‌تواند به بهبود زمان بارگذاری صفحه و کاهش CSS غیرضروری کمک کند.

## چرا CSS بلوک‌ها را غیرفعال کنیم؟

* **بهینه‌سازی عملکرد:** تعداد درخواست‌های HTTP و حجم کل CSS بارگذاری شده در وب‌سایت شما را کاهش می‌دهد، که منجر به زمان بارگذاری سریع‌تر صفحه می‌شود.
* **کد تمیزتر:** CSS را حذف می‌کند که ممکن است زائد باشد، اگر قالب یا صفحه ساز شما قبلاً استایل‌دهی خاص خود را برای عناصر رایج ارائه می‌دهد یا اگر از بلوک‌ها استفاده نمی‌کنید.
* **جلوگیری از تداخل:** به جلوگیری از تداخل‌های احتمالی استایل‌دهی بین CSS بلوک پیش‌فرض و CSS قالب یا صفحه ساز شما کمک می‌کند.
* **کنترل کامل:** به شما کنترل کاملی بر روی CSS بارگذاری شده در فرانت‌اند خود می‌دهد.

## قابلیت‌ها

* **حذف `wp-block-library.css`:** استایل‌دهی هسته بلوک‌های گوتنبرگ را حذف می‌کند.
* **حذف `wp-block-library-theme.css`:** استایل‌دهی پیش‌فرض بلوک‌های گوتنبرگ مختص قالب را حذف می‌کند.
* **حذف `wc-blocks-style.css`:** CSS بلوک‌های ووکامرس (مانند شبکه‌های محصول، بلوک‌های سبد خرید) را حذف می‌کند.
* در فرانت‌اند وب‌سایت شما اعمال می‌شود.

## نصب

برای پیاده‌سازی این کد، دو روش اصلی وجود دارد:

### روش ۱: به عنوان یک افزونه مستقل (توصیه شده)

ایجاد یک افزونه کوچک و اختصاصی، قوی‌ترین راه برای افزودن این قابلیت است. این تضمین می‌کند که تغییر شما صرف‌نظر از تغییر قالب، فعال باقی بماند.

1.  یک پوشه جدید با نام `wp-no-block-css` در مسیر `wp-content/plugins/` سایت وردپرسی خود ایجاد کنید.
2.  در داخل این پوشه جدید، یک فایل با نام `wp-no-block-css.php` ایجاد کنید.
3.  کد زیر را در `wp-no-block-css.php` کپی و جایگذاری کنید:

    ```php
    <?php
    /**
     * Plugin Name: WordPress Disable Block CSS
     * Description: Removes default Gutenberg and WooCommerce block CSS from the frontend for performance optimization.
     * Version: 1.0
     * Author: Your Name (Optional)
     * License: GPL-2.0-or-later
     */

    if ( ! defined( 'ABSPATH' ) ) {
        exit; // Exit if accessed directly.
    }

    /**
     * Dequeues default WordPress and WooCommerce block CSS files.
     */
    function mehdiamdev_remove_wp_block_library_css(){
        wp_dequeue_style( 'wp-block-library' );
        wp_dequeue_style( 'wp-block-library-theme' );
        wp_dequeue_style( 'wc-blocks-style' ); // Remove WooCommerce block CSS
    }
    add_action( 'wp_enqueue_scripts', 'mehdiamdev_remove_wp_block_library_css', 100 );
    ?>
    ```

4.  وارد پنل مدیریت وردپرس خود شوید، به بخش **"افزونه‌ها"** بروید و افزونه **"غیرفعال‌سازی CSS بلوک‌های وردپرس"** را **فعال کنید**.

### روش ۲: اضافه کردن به فایل functions.php قالب شما

می‌توانید این کد را مستقیماً به فایل `functions.php` قالب فعال خود اضافه کنید. **پیشنهاد اکید می‌شود قبل از انجام این کار، از فایل `functions.php` خود یک پشتیبان (backup) تهیه کنید.**

1.  به مسیر `wp-content/themes/YourThemeName/` بروید (به جای `YourThemeName` نام واقعی قالب فعال خود را قرار دهید).
2.  فایل `functions.php` را باز کنید.
3.  کد زیر را به انتهای فایل (قبل از تگ بستن `?>`، در صورت وجود) اضافه کنید:

    ```php
    /**
     * Dequeues default WordPress and WooCommerce block CSS files.
     */
    function mehdiamdev_remove_wp_block_library_css(){
        wp_dequeue_style( 'wp-block-library' );
        wp_dequeue_style( 'wp-block-library-theme' );
        wp_dequeue_style( 'wc-blocks-style' ); // Remove WooCommerce block CSS
    }
    add_action( 'wp_enqueue_scripts', 'mehdiamdev_remove_wp_block_library_css', 100 );
    ```

## ملاحظات مهم

* **تأثیر بصری:** **مهم است بدانید که اگر از بلوک‌های گوتنبرگ در صفحات یا نوشته‌های فرانت‌اند خود استفاده می‌کنید، حذف این فایل‌های CSS احتمالاً استایل‌دهی آن‌ها را مختل خواهد کرد.** اطمینان حاصل کنید که قالب یا صفحه ساز شما CSS لازم را برای هر بلوکی که استفاده می‌کنید فراهم می‌کند، یا به طور کامل از استفاده از بلوک‌ها در فرانت‌اند خودداری کنید.
* **بلوک‌های ووکامرس:** اگر از بلوک‌های جدیدتر ووکامرس (مانند در سبد خرید، تسویه‌حساب، یا صفحات فروشگاه) استفاده می‌کنید، حذف `wc-blocks-style` بر ظاهر آن‌ها تأثیر می‌گذارد. به طور کامل آزمایش کنید.
* **آزمایش:** همیشه پس از پیاده‌سازی این کد، سایت خود را به طور کامل آزمایش کنید تا مطمئن شوید هیچ مشکل بصری یا عملکردی به دلیل از دست رفتن CSS ایجاد نمی‌شود.

## مشارکت (Contributing)

مشارکت شما خوشایند است! اگر پیشنهاد یا بهبودهایی برای این کد دارید، می‌توانید یک "Pull Request" ایجاد کنید یا "Issue" جدیدی را گزارش دهید.

## مجوز (License)

این پروژه تحت مجوز GPL-2.0-or-later منتشر شده است.
