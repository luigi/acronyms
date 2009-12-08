# The Government Acronym Glossary

So you've decided to delve into the wonderful world of open government. Good for you, newly-minted civic hacker!

But soon you realize that there's a swamp of esoteric jargon to wade through. Sure, after a good bit of Googling, the haze starts to clear. Then you notice that the most insidious type of jargon is the acronym.

Everything related to government, either directly or tangentially, tends to have a long name. That long name gets shortened into an acronym that can collide with others. For example, MARC can refer to a [train system](http://www.mtamaryland.com/services/marc/), a [bibliographic standard](http://www.loc.gov/marc/), or a [regional planning group](http://www.marc.org/). One of the most important organizations in the transparency movement is commonly referred to as CRP, the Center for Responsive Politics, but a [Google search](http://www.google.com/search?q=CRP) hides the correct result all the way at the very bottom.

So we need something a bit better than Google, to help us solve this small, specific, but incredibly annoying problem.

## Development

This is a project slated for the [Great American Hackathon](http://www.sunlightlabs.com/hackathon09/), led by [Luigi Montanez](http://www.sunlightlabs.com/people/luigi/). It'll be a web app, similar in feel to the online dictionaries currently out there.

The plan is to host the app on [Google App Engine](http://code.google.com/appengine/), specifically using the [JRuby package](http://code.google.com/p/appengine-jruby/). This means that the app will be built with Sinatra and use DataMapper to access the datastore.

## Goals

The glossary encompasses:

* Government departments and agencies. All levels.
* Legislation, like BCRA and RICO.
* NGOs, not-for-profits, civic and business groups.
* Domain-specific jargon, like SSN and EIN.

The glossary will have two interfaces:

* A desktop web interface, using some standard templates.
* A mobile web interface, for optimized for iPhone and Android using [jqTouch](http://www.jqtouch.com/).

## Existing Resources

We'll need to scrape and load the following:

* [GovSpeak - Federal Agencies](http://members.cox.net/govdocs/govspeak.html)
* [State Department Glossary](http://www.aafsw.org/state/glossary1.htm)
* [Mid-America Regional Council Glossary](http://www.marc.org/acronyms.htm)


## Features

For the learning experience, we'll build everything using Behavior-Driven Development, so that means [Cucumber](http://cukes.info), [Webrat](http://wiki.github.com/brynary/webrat), [Shoulda](http://github.com/thoughtbot/shoulda) and supporting libraries.

Here are a few Cucumber-style stories to get us started:

    Scenario: Search for an existing acronym
      Given I am a site visitor
      When I go to the home page
      And I fill in "Search" with "FEC"
      And I press "Submit"
      Then I should see "Federal Election Commission"
      
    Scenario: Search for a missing acronym
      Given I am a site visitor
      When I go to the home page
      And I fill in "Search" with "FFC"
      And I press "Submit"
      Then I should see "Not found"
      
    Scenario: Submit a new acronym
      Given I am a site visitor
      When I go to the submit page
      And I fill in "Acronym" with "FFC"
      And I fill in "Full Name" with "Federal Fun Commission"
      And I fill in "Website" with "http://ffc.gov"
      And I fill in "Description" with "In charge of ensuring fun!"
      And I press "Submit"
      Then I should see "Thanks for your submission"

