<!--yml
category: 未分类
date: 2024-05-18 05:40:50
-->

# FX Trading Tile with Clojure/ClojureScript | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/07/22/fx-trading-tile-with-clojureclojurescript/#0001-01-01](https://mdavey.wordpress.com/2015/07/22/fx-trading-tile-with-clojureclojurescript/#0001-01-01)

Anyone who subscribes to any of my social network feeds would have seen an increase in Clojure noise over the last time period.  Clojure is interesting not just from a language perspective (Lisp) but from the few financial projects that have made the conferences over the last few years.  Although a niche language in many ways, it has a lot going for it, if like most things, you are prepared to invest a little time and effort.

What follows is my FX trading work in progress hack that will hopefully offer food for thought 😉

The main aim of the code hack was to get a simple FX currency pair tile in a browser built using [ClojureScript](http://cljs.info/cheatsheet/), backed by a [Clojure](https://www.niwi.nz/cljs-workshop/#_first_steps_with_ajax) server.  Starting point for the project as [lein-figwheel](https://github.com/bhauman/lein-figwheel/wiki/Quick-Start) with [Reagent](https://reagent-project.github.io/index.html).

Remember the code below (client followed by server code) has been hacked up, so ignore the hard coding et al.  The primary aim is as a learning tool, never to enter production 🙂

```
(ns ^:figwheel-always clojurefxtitle.core
    (:require
              [reagent.core :as reagent :refer [atom]]
              [clojurefxtitle.pricecomponent :as t]
    ))

(enable-console-print!)

(defonce app-state (atom {:text "FX Dashboard"
                        :counters {"USDGBP" {:id 1
                                             :name "USDGBP"}
                                   "USDEUR" {:id 2
                                             :name "USDEUR"}
                                   "USDJPY" {:id 3
                                             :name "USDJPY"}
                                  }
                          }))

(defn pricetitle-component []
  [:div
    ])

(defn fxtile [c]
  [:div {:style {:background "green" :width "300" :float "left" :border-style "solid"} }
    [:h1 {:style {:text-align "center" :margin "0" }} (:name c) ]
      [pricetitle-component]
        [:div
          [t/price-component (:name c)  "Buy"]
          [t/price-component (:name c)  "Sell"]
        ]
      ])

(defn dashboard []
  [:div {:style {:width "100%"} }
    (for [counter (vals (:counters @app-state))]
      ^{:key (:name counter)} [fxtile counter]
    )
  ]
)

(reagent/render-component [dashboard]
                          (. js/document (getElementById "app")))

(defn on-js-reload []
)

```

With the pricing component as per reference above, as follows:

```
(defn handler [response]
  (println "handler: " (str response))
)

(defn error-handler  [{:keys [status status-text]}]
  (println "error handler: " (str "something bad happened: " status " " status-text))
)

(defn my-click-handler [ccypair side price]
  (println (str "order " ccypair " " side " " price))
  (POST "/order"
          {:params {:price price
                    :side side
                    :ccypair ccypair}
           :handler handler
           :format :json
           :error-handler error-handler})    
  )

(defn rand-price [val]
  (rand-nth val))

(defn price-component [ccypair side]
  (let [seconds-elapsed (atom 0)
       whole_number (range 95000 100000)]
    (fn []
      (js/setTimeout #(reset! seconds-elapsed (rand-price whole_number)) 1000)
;;      (js/setTimeout #(swap! seconds-elapsed inc) 1000)
      (let [price (/ @seconds-elapsed 1000)]
        [:button {:style {:background "red" :width "150" :float "left" :text-align "center"}
           :on-click #(my-click-handler ccypair side price)}
         side (gstring/format " %0.3f" price )])))
       )

```

Clearly the code is using [atom’s](http://clojure.org/atoms), as one would expect. I had a few problems with the [JSON](http://udayv.com/clojure/2014/08/19/json-web-services-with-clojure/) web service “order” method, but ended up resolving the issue with [cljs-ajax](https://github.com/JulianBirch/cljs-ajax). Also using the [ring](https://github.com/ring-clojure/ring-json) server and handler to handle the routing.  Had a few issues with [http-kit](http://www.http-kit.org/server.html) deserialisation of the request, but I think that was partly my own silliness.

```
(ns server
  (:require
   [ring.middleware.resource :refer [wrap-resource]]
   [ring.middleware.json :as middleware]
   [ring.middleware.file-info :refer [wrap-file-info]]
   [ring.util.response :refer [redirect]]
   [compojure.handler :as handler]
   [compojure.core :refer :all]
   [compojure.route :as route]
   ))

(defn handler [request]
  (case (request :uri)
    "/" (redirect "index.html")
  )
)

(defn order-handler [req]
;;  (let [body (-> req :body)]
;;    (println "Request: " req " Body: " body)
;;  )
  (let [price (-> req :params :price)
    ccypair (-> req :params :ccypair)
    side (-> req :params :side)]
      (println (str "Order: " price side ccypair)) 
  )

  {:status 200 }
)  

(defroutes app-routes
  (GET "/" [] (redirect "index.html"))
  (POST "/order" [] order-handler) 
  (route/not-found "<h1>Custom - Page not found</h1>"))

(def app
  (-> (handler/api app-routes)
      (middleware/wrap-json-params)
      (middleware/wrap-json-response)))

```

Items to work on next:

*   Moving the simply price generator to the Clojure server, and streaming the prices via Websockets – possible using [chord](https://github.com/jarohen/chord) or [Sente](https://github.com/ptaoussanis/sente).
*   Look at [agents](http://clojure.org/agents) for the server.  [Avout](http://avout.io/) and [onyx](https://github.com/onyx-platform/onyx) also look interesting.
*   Dependency injection (e.g. [clj-di](https://github.com/nvbn/clj-di)) and MVC would be nice client side.

~ by mdavey on July 22, 2015.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/), [Trading](https://mdavey.wordpress.com/category/trading/)