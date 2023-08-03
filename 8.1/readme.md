# Laravel Test Runner - PHP 8.1

Docker Container with PHP 8.1 and extensions to be compatible with most Laravel applications. Also installed on this container we have Composer and NodeJS/NPM/Yarn.

## Building and pushing the image

**Build**:

```
docker build --pull -t jeffwray/laravel-test-runner .
```

**Tag**:

```
docker tag jeffwray/laravel-test-runner:latest jeffwray/laravel-test-runner:8.1
```

**Push**:

```
docker push jeffwray/laravel-test-runner:8.1
```

## Credits

- [Pushpak Chhajed](https://github.com/pushpak1300)

## Sponsorship

Development of this package is sponsored by Kirschbaum Development Group, a developer driven company focused on problem solving, team building, and community. Learn more [about us](https://jeffwray.com) or [join us](https://careers.jeffwray.com)!
