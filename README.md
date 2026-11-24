# Doctrine ORM 2.4.8 running clean on PHP 7.4, for EC-CUBE 3.0.x

EC-CUBE 3.0.18 requires `doctrine/orm` `<2.5`. Doctrine ORM 2.4 was written before PHP 7.4 and raises notices and a compile warning there. This fork keeps 2.4.8 and fixes those places.

## Fixed

| Where | What |
|---|---|
| `Query/Parser.php` (three places) | "Trying to access array offset on value of type null" when the lexer has no next token |
| `UnitOfWork.php` | `continue` inside a `switch` (PHP 7.3+ warns; replaced by `break`, which is what it always did) |

## Install

Requires Composer 2. In the shop's project root:

```
composer require nobuhiko/orm:^2.4.8
```

The package `replace`s `doctrine/orm` 2.4.8, so Composer removes the original and every other package keeps working against the same version.

## What this is, and is not

- The base is exactly the version EC-CUBE 3.0.18 ships. Nothing is upgraded; each fix is its own commit on the `eccube3/2.4` branch.
- Checked by running an EC-CUBE 3.0.18 shop (front pages, guest checkout to completion, contact form, admin screens) on PHP 7.1 and PHP 7.4 and comparing what PHP reports: with these changes PHP 7.4 reports nothing that PHP 7.1 does not.
- This is not an official release of the upstream project and is not supported by its maintainers. Upstream: https://github.com/doctrine/orm
- EC-CUBE 3 が使っているバージョンのまま、PHP 7.4 で出る注意と警告だけを直したものです。保守: うみうしラボ
