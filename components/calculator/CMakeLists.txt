set(srcs "calculator.c")
set(dirs ".")

 if(CONFIG_TEST_DOUBLE)
     list(APPEND srcs "./mocks/mock_math.c")
     list(APPEND dirs "./mocks")
 endif()

idf_component_register(SRCS "${srcs}"
                     INCLUDE_DIRS "${dirs}"
                     )

#includeしているのはmath.hでも、明示的にtest_math.hをリンクして、同名の関数を定義しておけばオーバーライドできる
#buildはesp-idfの構成を使っているが、platformioのtest機能は、unityを使っているが、テストアプリのbuildはplatformio側で構成している。esp-idfの構成（componentsにtestを含める）が使えない。と思う。
#Kconfigで設定した定数で、ビルドを変更する場合は、定数にCONFIG_をつけて参照すること