=== WooCommerce Order Delivery ===
Contributors: upss1988

Updating instruction

Changed Path:
- /includes/admin/fields/class-wc-od-admin-field-delivery-days.php
- /templates/emails/email-delivery-date.php #34
- /templates/order/delivery-date.php #40
- /includes/admin/class-wc-od-admin-settings.php #422
- /templates/checkout/form-delivery-date.php #24
- p.form-field._delivery_time_frame_field { display: none; }

*** /includes/admin/fields/class-wc-od-admin-field-delivery-days.php
    Remove this part of code on #34 line
    ```
    printf(
        '<p><strong>%1$s</strong> %2$s</p>',
        esc_html__( 'Time frames:', 'woocommerce-order-delivery' ),
        wp_kses_post( join( ' | ', $time_frames ) )
    );
    ```

*** /templates/emails/email-delivery-date.php
    Remove this part of code on #40 line
    ```
    <?php
        /* translators: %s: delivery time frame */
        printf( wp_kses_post( __( 'Time frame: %s', 'woocommerce-order-delivery' ) ), '<strong>' . wc_od_time_frame_to_string( $delivery_time_frame ) . '</strong>' ); // WPCS: XSS ok.
    ?>
    ```

*** /templates/order/delivery-date.php
    Remove this line of code on #40 line
    ```
    <?php
        /* translators: %s: delivery time frame */
        printf( wp_kses_post( __( 'Time frame: %s', 'woocommerce-order-delivery' ) ), '<strong>' . wc_od_time_frame_to_string( $delivery_time_frame ) . '</strong>' ); // WPCS: XSS ok.
    ?>
    ```

*** /includes/admin/class-wc-od-admin-settings.php
    Customize object inside get_settings() method
    array with id wc_od_maybe_prefix( 'checkout_delivery_option' )

    Add this part of code inside 'options' => array():
    ```
    'disable' => __( 'Disable checkout options', 'woocommerce-order-delivery' ),
    ```

*** /templates/checkout/form-delivery-date.php
    Add below condition above the <?php if ( 'calendar' === $delivery_option ) : ?>
    ```
    <?php if ( 'disable' === $delivery_option ) : ?>
        <style>
            div#wc-od{display: none!important;}
        </style>
    <?php endif; ?>
    ```

*** p.form-field._delivery_time_frame_field { display: none; }
    Add this CSS elsewhere ( you can inside CSS & JS plugin)
    ```
    p.form-field._delivery_time_frame_field { display: none; }
    ```