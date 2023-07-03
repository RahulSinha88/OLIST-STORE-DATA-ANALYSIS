create database olistStore;
use olistStore;
show tables;

-- INSERTING TABLES
select * from olist_customers_dataset;   
select * from olist_geolocation_dataset;
select * from olist_order_items_dataset;
select * from olist_order_payments_dataset;
select * from olist_order_reviews_dataset;
select * from olist_orders_dataset;
select * from olist_products_dataset;
select * from olist_sellers_dataset;
select * from product_category_name_translation;


-- 1). WEEKDAY VS WEEKEND PAYMENT STATISTICS:
       SELECT 
       CASE WHEN weekday(order_purchase_timestamp) BETWEEN 1 AND 5 THEN 'Weekday'
       ELSE 'Weekend' END AS day_type,
       round(sum(payment_value),2) AS num_payments
       FROM olist_orders_dataset od join olist_order_payments_dataset pd on od.order_id = pd.order_id
	   GROUP BY day_type; 
       
      

-- 2).Number of Orders with review score 5 and payment type as credit card
      select    
      COUNT(*) AS num_people
      from olist_order_reviews_dataset o inner join olist_order_payments_dataset p on o.order_id = p.order_id
      WHERE review_score = 5 
      AND payment_type = "credit_card" ;


-- 3) Average number of days taken for order_delivered_customer_date for pet_shop
		 with dd as
		(select timestampdiff(day,order_purchase_timestamp,order_delivered_customer_date) as avg_days , product_id
        from olist_orders_dataset od inner join olist_order_items_dataset id on od.order_id = id.order_id )
		select avg_days from dd inner join olist_products_dataset pd on dd.product_id = pd.product_id 
        where product_category_name = "pet shop";



-- 4) Average price and payment values from customers of sao paulo city
         
         select concat(format(avg(price),2)) as avg_price,concat(format(avg(payment_value),2)) as avg_payment_value 
         from olist_order_payments_dataset 
		 inner join olist_order_items_dataset on olist_order_payments_dataset.order_id = olist_order_items_dataset.order_id
         inner join olist_orders_dataset on olist_order_items_dataset.order_id = olist_orders_dataset.order_id
         inner join olist_customers_dataset on olist_orders_dataset.customer_id = olist_customers_dataset.customer_id 
         where customer_city="sao paulo";



-- 5) Relationship between shipping days (order_delivered_customer_date - order_purchase_timestamp) Vs review scores.
      
       with dd as
       (select *,
       timestampdiff(day,order_purchase_timestamp,order_delivered_customer_date) as delivery_days
       from olist_orders_dataset )
       select delivery_days,count(review_score) from dd 
       inner join olist_order_reviews_dataset on dd.order_id = olist_order_reviews_dataset.order_id
       group by delivery_days;



     






