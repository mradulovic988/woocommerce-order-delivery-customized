<!-- PROJECT LOGO -->
<br />
<p align="center">

  <h1 align="center">WooCommerce Order Delivery - Customized</h1>

  <p align="left">
    * Contributors: upss1988
    <br />
  </p>
  
  <p align="center">
    Documentation ( Depending of current version of the plugin )
    <br />
  </p>
</p>


<!-- Path to be changed -->
## Path to be changed

- /includes/admin/fields/class-wc-od-admin-field-delivery-days.php
- /templates/emails/email-delivery-date.php #34
- /templates/order/delivery-date.php #40
- /includes/admin/class-wc-od-admin-settings.php #422
- /templates/checkout/form-delivery-date.php #24
- p.form-field._delivery_time_frame_field { display: none; }


<!-- /includes/admin/fields/class-wc-od-admin-field-delivery-days.php -->
## /includes/admin/fields/class-wc-od-admin-field-delivery-days.php
Remove this part of code on #34 line:
```
printf(
    '<p><strong>%1$s</strong> %2$s</p>',
    esc_html__( 'Time frames:', 'woocommerce-order-delivery' ),
    wp_kses_post( join( ' | ', $time_frames ) )
);
```

<!-- /templates/emails/email-delivery-date.php -->
## /templates/emails/email-delivery-date.php
Remove this part of code on #40 line:
```
/* translators: %s: delivery time frame */
printf( wp_kses_post( __( 'Time frame: %s', 'woocommerce-order-delivery' ) ), '<strong>' . wc_od_time_frame_to_string( $delivery_time_frame ) . '</strong>' ); // WPCS: XSS ok.
```

<!-- /templates/order/delivery-date.php -->
## /templates/order/delivery-date.php
Remove this part of code on #40 line:
```
/* translators: %s: delivery time frame */
printf( wp_kses_post( __( 'Time frame: %s', 'woocommerce-order-delivery' ) ), '<strong>' . wc_od_time_frame_to_string( $delivery_time_frame ) . '</strong>' ); // WPCS: XSS ok.
```

<!-- /includes/admin/class-wc-od-admin-settings.php -->
## /includes/admin/class-wc-od-admin-settings.php
Customize object inside get_settings() method

array with id wc_od_maybe_prefix( 'checkout_delivery_option' )

```
'disable' => __( 'Disable checkout options', 'woocommerce-order-delivery' ),
```

<!-- /templates/checkout/form-delivery-date.php -->
## /templates/checkout/form-delivery-date.php
Add below condition above the `<?php if ( 'calendar' === $delivery_option ) : ?>`

```
<?php if ( 'disable' === $delivery_option ) : ?>
    <style>
        div#wc-od{display: none!important;}
    </style>
<?php endif; ?>
```

<!-- CSS -->
## CSS
Add this CSS elsewhere ( you can inside CSS & JS plugin)

```
p.form-field._delivery_time_frame_field { 
    display: none; 
}
```



<!-- CONTRIBUTING -->
## Contributing

* upss1988


<!-- LICENSE -->
## License

Distributed under GNU General Public License v3.0. See `LICENSE` for more information.



<!-- CONTACT -->
## Contact

<p>Author: Marko Radulovic </p>
<p>Find me on: <a href="https://www.linkedin.com/in/marko-radulovic/" target="_blank">LinkedIn</a></p>
<p>Email: <a href="mailto:upss070288@gmail.com">upss070288@gmail.com</a></p>