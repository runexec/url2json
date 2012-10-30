````clojure
(ns url2json.core
  (:require [cheshire.core :as JSON]))

(defn url2json
  [url]
  (JSON/generate-string
   (hash-map :_data
             (with-open [rdr
                         (clojure.java.io/reader url)]
               (reduce
                #(clojure.string/join "\n" %&)
                (line-seq rdr))))
   {:escape-non-ascii true}))
````