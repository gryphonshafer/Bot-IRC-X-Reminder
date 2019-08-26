# NAME

Bot::IRC::X::Reminder - Bot::IRC plugin for scheduling reminders

# VERSION

version 1.04

[![Build Status](https://travis-ci.org/gryphonshafer/Bot-IRC-X-Reminder.svg)](https://travis-ci.org/gryphonshafer/Bot-IRC-X-Reminder)
[![Coverage Status](https://coveralls.io/repos/gryphonshafer/Bot-IRC-X-Reminder/badge.png)](https://coveralls.io/r/gryphonshafer/Bot-IRC-X-Reminder)

# SYNOPSIS

    use Bot::IRC;

    Bot::IRC->new(
        connect => { server => 'irc.perl.org' },
        plugins => ['Reminder'],
    )->run;

# DESCRIPTION

This [Bot::IRC](https://metacpan.org/pod/Bot::IRC) plugin is for scheduling reminders. You can ask the bot to
remind someone about something at some future time. If the nick who needs to
be reminded isn't online at the time of the reminder, the reminder isn't issued.

The general format is:

    <bot nick> remind <nick|channel> <every|at|in> <time expr> <reminder text>

If you specify a "nick" of "me", then the bot will remind your nick.

The "every|at|in" is the type of reminder. Each type of reminder requires a
slightly different time expression.

## at

The "at" reminder type requires a time expression in the form of a clock time
or a crontab-looking expression. Clock time expressions are in the form
`\d{1,2}:\d{2}\s*[ap]m?` for "normal human time" and `\d{3,4}` for military
time.

    bot remind me at 2:30p This is to remind you of your dentist appointment.
    bot remind hoser at 1620 Hey hoser, it's 4:20 PM now.
    bot remind #team at 0530 Time for someone on the team to make coffee.

Crontab-looking expressions are in the `* * * * *` form.

    bot remind me at 30 5 * * 1-5 Good morning! It's a great day to code Perl.

Once an "at" reminder type triggers, it's done and won't repeat.

## in

The "in" reminder type requires a number of minutes in the future for when the
reminder should happen. In addition to minutes, you can specify hours, days,
weeks, or whatever.

    bot remind me in 30 It has been half-an-hour since you set this reminder.
    bot remind me in 2:30 It has been 2 hours and 30 minutes.
    bot remind me in 3:0:0 It has been 3 days.
    bot remind me in 1:2:0:0 It has been 1 week and 2 days.

Once an "in" reminder type triggers, it's done and won't repeat.

## every

The "every" reminder type is exactly like the "at" reminder type except that
the reminder repeatedly triggers when the time expression matches.

    bot remind me every 30 5 * * 1-5 Another great day to code Perl.

# HELPER FUNCTIONS

There are a couple of helper functions you can call as well.

## list reminders

You can list all of your reminders or all reminders from anyone.

    bot reminders list mine
    bot reminders list all

## forget reminders

You can tell the bot to forget all of your reminders or all reminders from
everyone.

    bot reminders forget mine
    bot reminders forget all

# SEE ALSO

You can look for additional information at:

- [Bot::IRC](https://metacpan.org/pod/Bot::IRC)
- [GitHub](https://github.com/gryphonshafer/Bot-IRC-X-Reminder)
- [CPAN](http://search.cpan.org/dist/Bot-IRC-X-Reminder)
- [MetaCPAN](https://metacpan.org/pod/Bot::IRC::X::Reminder)
- [AnnoCPAN](http://annocpan.org/dist/Bot-IRC-X-Reminder)
- [Travis CI](https://travis-ci.org/gryphonshafer/Bot-IRC-X-Reminder)
- [Coveralls](https://coveralls.io/r/gryphonshafer/Bot-IRC-X-Reminder)
- [CPANTS](http://cpants.cpanauthors.org/dist/Bot-IRC-X-Reminder)
- [CPAN Testers](http://www.cpantesters.org/distro/T/Bot-IRC-X-Reminder.html)

# AUTHOR

Gryphon Shafer <gryphon@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2018 by Gryphon Shafer.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
