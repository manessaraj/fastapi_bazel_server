load("@io_bazel_rules_docker//python3:image.bzl", py_image = "py3_image")
load("@io_bazel_rules_docker//container:container.bzl", "container_push")

py_binary(
    name="main",
    deps=[
        "@pip_uvicorn//:pkg",
        "@pip_fastapi//:pkg"
    ],
    srcs=["main.py"],
    
)

py_library(
    name="app",
    srcs=[
        "__init__.py"
    ]
)

py_image(
    name="main_image",
    deps=[
        "@pip_uvicorn//:pkg",
        "@pip_fastapi//:pkg",
        ":main"
    ],
    main="main.py",
    srcs=["main.py"],
)


container_push(
    name = "fastapi_server",
    format = "Docker",
    image = ":main_image",
    registry = "index.docker.io",
    repository = "smanes/fastapi",
    tag = "1",
)