# Elementor Loop Dynamic Lightbox
A workaround for opening dynamic video links in a lightbox in Elementor Loops. Useful, because the lightbox functionality in Elementor doesn't include the option to add dynamic data, such as data from ACF custom fields.

As of November 2023, Elementor's native elementorFrontend.utils.lightbox.showModal method is unavailable, requiring a 3rd party lightbox.

## Prerequisites

- A Custom Post Type with an ACF URL Custom Field for video links (e.g., YouTube links).
- Elementor Pro with Loop functionality.

## Setup Instructions

### 1. Configure Your Loop

Edit your loop to include an element that acts as a link. This could be a text block, image, or the loop container itself.

To setup the loop container as a link:
- Go to **Layout > Additional Options > HTML Tag** and select `a` (link).
- Ensure the loop item contains no other links.

Add the links:
- Use the dynamic tags feature (database icon) to insert the ACF URL Custom Field which contains your video link.

### 2. Add the Required Class

Assign the class `js-video-lightbox` to the element with the link.
- Navigate to **Advanced > CSS Classes** and input `js-video-lightbox`.

### 3. Insert Custom Script

Go to **Elementor > Custom Scripts** and add the following JavaScript code:

```javascript
<script>
jQuery(document).ready(function($) {
    $('a.js-video-lightbox').on('click', function(e) {
        e.preventDefault(); // Prevents default link action
        $(this).magnificPopup({
            type: 'iframe'
        }).magnificPopup('open');
    });
});
</script>
```

Set display conditions to include only pages where this script is needed to optimize loading speeds.

### 4. Load Magnific Popup Library

Include the Magnific Popup library by adding the following code to your theme's functions.php file:

```php
function enqueue_magnific_popup() {
    wp_enqueue_style('magnific-popup-css', '//cdnjs.cloudflare.com/ajax/libs/magnific-popup.js/1.1.0/magnific-popup.min.css');
    wp_enqueue_script('magnific-popup-js', '//cdnjs.cloudflare.com/ajax/libs/magnific-popup.js/1.1.0/jquery.magnific-popup.min.js', array('jquery'));
}
add_action('wp_enqueue_scripts', 'enqueue_magnific_popup');
```
