E-Commerce

    - Website -
                 Clicks the product link [topic "clicks"]
                 one add item to shopping cart
                                [topic: "cart"]
                 buys the product
                                [topic: 'orders']
    - Web Services [logs, ]
    - Mobile Apps

    - Email [consumer, orders]
    - SMS/Text [consumer, orders]
    - Shipping[consumer, orders]
    ...

    -- recommendation engine(clicks, cart, orders)


Topic (clicks) ==> M0, M1, M2, M3....M1000000000000
    WHY ? 1 TB
        Broker 1 : 250 GB SSD/NVMe [No Space]

        Brokers (10 Brokers)
            each has 250 GB SSD (up to 2.5 TB)

            Partition (4 no), each one has 
                    (P0 ==> 300 GB
                     P1 ==> 200 GB
                     P2 ==> 250 GB
                     P3 ==> 250 GB

            Partition (10 no), each one has 
                    (P0 ==> 300 GB
                     P1 ==> 200 GB
                     P2 ==> 250 GB
                     P3 ==> 250 GB

Partition (sub set of topic messages) (4 partitions)

    Partition 0 [M0, M4, M8, M12, .....] 300 GB
    Partition 1 [M1, M5,  M9, M13, .....] 200 GB
    Partition 2 [M2, M5, M10, M14, .....] 250 GB
    Partition 3 [M3, M6, M11, M15, .....] 250 GB

Partition (1 partitions)

    Partition 0 [M0, M1, M2, M3....M1000000000]

Partition (2 partitions)
     Partition 0 [M0, M2, M4, M6, M8,....]
     Partition 1 [M1, M3, M5, M7....]



Partition (sub set of topic messages) (4 partitions)

    Partition 0 [M0, M10, M20, .....] 100 GB
    Partition 1 [M1, M11, M21, .....] 50 GB
    Partition 2 [M2, M22, , .....] 75 GB
    Partition 3 [ .....] 25 GB
    Partition 4 [  .....] 60 GB
      ...
    Partition 9 [M3, M6, M11, M15, .....] 50 GB