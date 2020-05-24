Here you’ll find a codebook explaining the database structure for the
Undressing IG project.

# Setup

Follow the steps below in a terminal to load the database from a dump
file and save under the name `igdb`.

    pg_restore 02-19_backup > backup.sql
    sudo -i -u postgres
    dropdb igdb
    createdb igdb
    igdb < backup.sql

Load packages needed

``` r
library("RPostgreSQL")
```

Read database

``` r
# create a connection to the postgres database
con = dbConnect(dbDriver("PostgreSQL"), dbname= "igdb", host="127.0.0.1", user="postgres", password = params$pwd)

#list tables in the database
dbListTables(con)
```

    ##  [1] "auth_user_user_permissions"    "data_donors_datadonationerror" "django_migrations"            
    ##  [4] "django_session"                "auth_permission"               "auth_group"                   
    ##  [7] "django_content_type"           "auth_user_groups"              "auth_user"                    
    ## [10] "data_donors_donor"             "data_donors_datadonation"      "data_donors_donor_following"  
    ## [13] "data_donors_donorfollowing"    "data_donors_encounter"         "django_admin_log"             
    ## [16] "ig_observer_igpost"            "ig_observer_igimage"           "auth_group_permissions"       
    ## [19] "ig_observer_iguser"            "ig_observer_gvisionanalyse"

# Codebook

## data\_donors\_donor\_following

Observed accounts each donor follows

`id` Pair ID

`donor_id` Donor ID

`iguser_id` Observed account ID

## data\_donors\_datadonation

Log of donation runs

`id` Encounter ID

`created` Encounter time

`ig_posts_seen` Number of IG posts seen (12 normally)

`donor_id` Donor ID

## data\_donors\_encounter

Log of encounters with posts from observed accounts

`id` Encounter ID

`position_in_list` Position of encounter in the user feed. Starts
counting at 0

`data_donation_id` ID of donation run

`ig_post_id`

## data\_donors\_donor

List of donors

`id`

`ig_donor_id`

`created`

`last_status`

`last_status_changed`

`version`

`updated`

`display_name`

## data\_donors\_donorfollowing

List of accounts the donor follows, encountered in the feed during
donation runs

`id`

`created`

`following_ig_username`

`donor_id`

## ig\_observer\_igimage

List of images in observed posts

`id` Image ID

`image_url` Image URL

`ig_post_id` Post ID

## ig\_observer\_iguser

List of details for observed IG accounts.

`id` Account ID

`created` Timestamp of observation creation

`ig_username` Username

`created_by_id` Observation created by

`ig_biography` IG Bio

`ig_business_category_name` Business category

`ig_full_name` Full name

`ig_id` IG User ID

`ig_is_business_account` Is business account?

`ig_profile_pic` URL of profile pic

`sex` Gender of user m or f

## ig\_observer\_gvisionanalyse

Result of G Vision analysis

`id`

`analyse`

`ig_image_id`

`created`

## ig\_observer\_igpost

List of posts by observed accounts

`id` Post ID

`created` Encountered timestamp

`ig_id` IG ID

`ig_shortcode` IG Shortcode

`ig_taken_at_timestamp` IG picture timestamp

`ig_type` Type: Image, Video, Image gallery

`ig_user_id`

`created_by_donor`
