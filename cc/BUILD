package(default_visibility = ["//visibility:public"])

load("@io_bazel_rules_docker//container:container.bzl", "container_image")
load("@package_bundle//file:packages.bzl", "packages")
load("@package_bundle_debian10//file:packages.bzl", packages_debian10 = "packages")

DISTRO_PACKAGES = {
    "": packages,
    "-debian10": packages_debian10,
}

# An image for C/C++ programs
[[container_image(
    name = ("cc" if (not mode) else mode[1:]) + distro_suffix,
    base = "//base" + (mode if mode else ":base") + distro_suffix,
    debs = [
        DISTRO_PACKAGES[distro_suffix]["libgcc1"],
        DISTRO_PACKAGES[distro_suffix]["libgomp1"],
        DISTRO_PACKAGES[distro_suffix]["libstdc++6"],
    ],
) for mode in [
    "",
    ":debug",
]] for distro_suffix in ("", "-debian10")]
