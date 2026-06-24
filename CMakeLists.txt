cmake_minimum_required(VERSION 3.14)

project(KakeiboApp)

set(CMAKE_CXX_STANDARD 17)

# 共通ライブラリ
add_library(
    kakeibo_lib
    src/sample_code.cpp
)

# アプリ本体
add_executable(
    app
    src/main.cpp
)

target_link_libraries(
    app
    kakeibo_lib
)

#GoogleTestをMddでビルドするための設定
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
# GoogleTest取得
include(FetchContent)

FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/refs/tags/v1.14.0.zip
)

FetchContent_MakeAvailable(googletest)

# テスト実行ファイル
add_executable(
    unit_test
    tests/sample_test.cpp
)

target_link_libraries(
    unit_test
    kakeibo_lib
    GTest::gtest_main
)