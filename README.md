# NAME

DateTimeX::Factory - DateTime factory module with default timezone.

# VERSION

This document describes DateTimeX::Factory version 0.03.

# SYNOPSIS

    use DateTimeX::Factory;

    #Object interface
    my $factory = DateTimeX::Factory->new(
        time_zone => 'Asia/Tokyo',
    );
    my $now = $factory->now;

    #Class interface
    DateTimeX::Factory->set_time_zone(DateTime::TimeZone->new(name => 'Asia/Tokyo'));
    my $now = DateTimeX::Factory->now;

# DESCRIPTION

DateTime factory module with default timezone.
This module include wrapper of default constructors and some useful methods.

# METHODS

## `set_time_zone($time_zone)`

If called as instance method, set time\_zone for its factory instance methods.
If called as class method, set time\_zone for class methods.

    #Object interface
    {
        my $factory = DateTimeX::Factory->new();
        say $factory->now->time_zone->name; # floating

        $factory->set_time_zone(DateTime::TimeZone->new(name => 'Asia/Tokyo'));
        say $factory->now->time_zone->name; # Asia/Tokyo

        #This is also OK
        $factory->set_time_zone('Asia/Tokyo');
        say $factory->now->time_zone->name; # Asia/Tokyo

        # set to default time zone (floating)
        $factory->set_time_zone;
    }

    #Class interface
    {
        DateTimeX::Factory->set_time_zone(DateTime::TimeZone->new(name => 'Asia/Tokyo'));
        say DateTimeX::Factory->now->time_zone->name; #Asia/Tokyo

        #This is also OK
        DateTimeX::Factory->set_time_zone('Asia/Tokyo');
        say DateTimeX::Factory->now->time_zone->name; #Asia/Tokyo

        # set to default time zone (floating)
        DateTimeX::Factory->set_time_zone;
    }

## `get_time_zone($time_zone)`

Get DateTime::TimeZone instance of current time zone.

## `create(%params)`

Call DateTime->new with default parameter.

    my $datetime = DateTimeX::Factory->create(year => 2012, month => 1, day => 24, hour => 23, minute => 16, second => 5);

## `now(%params)`, `today(%params)`, `from_epoch(%params)`, `last_day_of_month(%params)`, `from_day_of_year(%params)`

See document of [DateTime](http://search.cpan.org/perldoc?DateTime).
But, these methods create DateTime instance by original method with default parameter.

## `strptime($string, $pattern)`

Parse string by DateTime::Format::Strptime with default parameter.

    my $datetime = DateTimeX::Factory->strptime('2012-01-24 23:16:05', '%Y-%m-%d %H:%M:%S');

## `from_mysql_datetime($string)`

Parse MySQL DATETIME string with default parameter.

    #equals my $datetime = DateTimeX::Factory->strptime('2012-01-24 23:16:05', '%Y-%m-%d %H:%M:%S');
    my $datetime = DateTimeX::Factory->from_mysql_datetime('2012-01-24 23:16:05');

## `from_mysql_date($string)`

Parse MySQL DATE string with default parameter.

    #equals my $date = DateTimeX::Factory->strptime('2012-01-24', '%Y-%m-%d');
    my $date = DateTimeX::Factory->from_mysql_date('2012-01-24');

## `from_ymd($string, $delimiter)`

Parse string like DateTime::ymd return value with default parameter.

    #equals my $date = DateTimeX::Factory->strptime('2012/01/24', '%Y/%m/%d');
    my $date = DateTimeX::Factory->from_ymd('2012-01-24', '/');

## `tommorow(%params)`

Create next day DateTime instance.

    #equals my $tommorow = DateTimeX::Factory->today->add(days => 1);
    my $tommorow = DateTimeX::Factory->tommorow;

## `yesterday(%params)`

Create previous day DateTime instance.

    #equals my $yesterday = DateTimeX::Factory->today->subtract(days => 1);
    my $yesterday = DateTimeX::Factory->yesterday;

# DEPENDENCIES

Perl 5.10.0 or later.
[Data::Validator](http://search.cpan.org/perldoc?Data::Validator)
[DateTime](http://search.cpan.org/perldoc?DateTime)
[DateTime::Format::MySQL](http://search.cpan.org/perldoc?DateTime::Format::MySQL)
[DateTime::Format::Strptime](http://search.cpan.org/perldoc?DateTime::Format::Strptime)
[DateTime::TimeZone](http://search.cpan.org/perldoc?DateTime::TimeZone)
[Mouse](http://search.cpan.org/perldoc?Mouse)

# BUGS

All complex software has bugs lurking in it, and this module is no
exception. If you find a bug please either email me, or add the bug
to cpan-RT.

# SEE ALSO

[perl](http://search.cpan.org/perldoc?perl)

# AUTHOR

Nishibayashi Takuji <takuji@senchan.jp>

# LICENSE AND COPYRIGHT

Copyright (c) 2012, Nishibayashi Takuji. All rights reserved.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.