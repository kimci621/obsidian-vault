
**#tilda-frontpad-cart**

  

  

    function convertTimeFormat(time) {

        if (!time) {

            return ''

        }

  

        const date = new Date();

        const year = date.getFullYear();

        const month = String(date.getMonth() + 1).padStart(2, '0');

        const day = String(date.getDate()).padStart(2, '0');

        const formattedDate = `${year}-${month}-${day}`;

        const convertedTimeString = `${formattedDate} ${time}:00`;

  

        return convertedTimeString || ''

    }

  

    function newOrder(order_data, cart_items) {

        if (!order_data) {

          return

        }

        if (!cart_items) {

          return

        }

        // number[]

        let product_sku_items = [];

        // number[]

        let product_count_items = [];

        cart_items?.products?.forEach((product) => {

          product_sku_items.push(Number(product.sku));

          product_count_items.push(Number(product.quantity));

        });

        console.log(cart_items, product_sku_items, product_count_items)

  

        const url = "https://app.frontpad.ru/api/index.php?new_order";

        let secret = "6rG744HFH2AFshdb7aGDzaFdaKhSeaRark7edFNNsafKhkNekhGKiaRkN25S2HSdYNi3e2BA2H88YKb8YHG6Kkek9952HH5sibfs4HRReQN4nR28ny53G9aG96tGDk3Qn76dEHTKkyBBakzrHrdereNn97YDfKdzF8D9GiHTG9hGkGZYZ43a7Dr7AazFKD5eAtd7EQR9N2G2tsGehzed2z9izzS72Kak5efzT2ztN5e6iQatafA3EAa3YS";

        // артикулы товаров в корзине [articul, articul, articul]

        const product = product_sku_items;

        // кол-во товара [count, count, count]

        const product_kol = product_count_items;

        // улица, длина до 50 знаков;

        const street = order_data.street.slice(0, 50) || "";

        // дом, длина до 50 знаков;

        const home = order_data.home.slice(0, 50) || "";

        // подъезд, длина до 2 знаков;

        const pod = order_data.pod.slice(0, 2) || "";

        // этаж, длина до 2 знаков;

        const et = order_data.et.slice(0, 2) || "";

        // квартира, длина до 50 знаков;

        const apart = order_data.apart.slice(0, 50) || "";

        // телефон, длина до 50 знаков;

        const phone = order_data.phone.slice(0, 50) || "";

        // примечание, длина до 100 знаков;

        const descr = order_data.descr.slice(0, 100) || "";

        // имя клиента, длина до 50 знаков;

        const name = order_data.name.slice(0, 50) || "";

        // тип оплаты заказа, значение можно посмотреть в справочнике “Варианты оплаты”

        const pay = order_data.pay === 'Б/нал.' ? '2' : '1';

        // количество персон, длина 2 знака

        const person = order_data.person.slice(0, 2) || "";

        // время “предзаказа”, указывается в формате ГГГГ-ММ-ДД ЧЧ:ММ:СС, например 2016-08-15 15:30:00

        const datetime = convertTimeFormat(order_data.datetime) || "";

        console.log("product:", product);

        console.log("product_kol:", product_kol);

        console.log("street:", street);

        console.log("home:", home);

        console.log("pod:", pod);

        console.log("et:", et);

        console.log("apart:", apart);

        console.log("phone:", phone);

        console.log("descr:", descr);

        console.log("name:", name);

        console.log("pay:", pay);

        console.log("person:", person);

        console.log("datetime:", datetime);

  

        const formData = new FormData();

        if (secret) formData.append("secret", secret)

        if (street) formData.append("street", street);

        if (home) formData.append("home", home);

        if (pod) formData.append("pod", pod);

        if (et) formData.append("et", et);

        if (apart) formData.append("apart", apart);

        if (phone) formData.append("phone", phone);

        if (descr) formData.append("descr", descr);

        if (name) formData.append("name", name);

        if (pay) formData.append("pay", pay);

        if (person) formData.append("person", person);

        if (datetime) formData.append("datetime", datetime);

  

        if (product.length) {

            product.forEach(p => {

                formData.append("product[]", p);

            })

        }

        if (product_kol.length) {

            product_kol.forEach(pk => {

                formData.append("product_kol[]", pk)

            })

        }

        if (!axios) {

            console.log('axios is not installed')

            return

        }

  

        axios.post(url, formData)

          .then((response) => response.data)

          .then((result) => {

            console.log(result);

            // Обработка успешного ответа API

            if (result.result === 'success') {

              console.log('Успешный заказ:', result);

            }

            // Обработка ошибки API

            else if (result.result === 'error') {

              console.log('Ошибка заказа:', result);

            }

            // Обработка предупреждений API

            else if (result.warnings) {

              console.log('Предупреждения:', result);

            }

          })

          .catch((error) => {

            console.error('Ошибка при отправке заказа:', error);

          });

  

    }

  

    async function mySuccessFunction(form) {

        if (!form) return;

        if (form instanceof jQuery) {

          form = form.get(0);

        }

  

        // Товары из корзины (неформатированные)

        var cart_items = JSON.parse(localStorage.getItem('tcart'))

        // Объект корзины

        var obj = {};

        // Поля формы корзины

        var inputs = form.elements;

        Array.prototype.forEach.call(inputs, function (input) {

          if (input.type === 'radio') {

            if (input.checked) obj[input.name] = input.value;

          } else {

            obj[input.name] = input.value;

          }

        });

  

       localStorage.setItem('last-order', JSON.stringify(obj))

       await newOrder(obj, cart_items)

      }

  

      if (document.readyState !== 'loading') {

        us_sendFormAfterSuccess();

      } else {

        document.addEventListener('DOMContentLoaded', us_sendFormAfterSuccess);

      }

  

      function us_sendFormAfterSuccess() {

        var forms = document.querySelectorAll('.js-form-proccess');

        Array.prototype.forEach.call(forms, function (form) {

          form.addEventListener('tildaform:aftersuccess', function (e) {

            e.preventDefault();  

            mySuccessFunction(form);

          });

          form.addEventListener('submit', function (e) {

            e.preventDefault();

          });

        });

      }

  

  

  

  

Timer popup

<a class="toolate" href="#popup:toolate" role="button" aria-haspopup="dialog"></a>

<script defer="" type="text/javascript">

   var day = new Date();

   var hour = day.getHours();

   var numday = day.getDay();

 $(document).ready(function () {

    if ( hour >= 23 || hour < 11) {

     setTimeout(function () {$('.toolate')[0].click(); }, 5000);

    };

 });  

</script>