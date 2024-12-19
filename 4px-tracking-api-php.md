4PX Tracking API - PHP
================================
Use PHP to track 4PX shipments with 4PX Tracking API.

Features
--------
- Real-time 4PX tracking.
- Batch 4PX tracking.
- Other features to manage your 4PX tracking.

Installation
------------

Installation is easy:

    $ composer require trackingmore/trackingmore-sdk-php

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your 4PX shipments.

Usage
----------

Create a tracking (Real-time tracking):

      require('vendor/autoload.php');

      use Trackingmore\TrackingMoreException;
      use TrackingMore\Trackings;
        
      $key = 'your api key';
      $response = null;
      $trackings = new Trackings($key);
      
      try {
        $params = ['tracking_number'=>'4PX3001518625089CN','courier_code'=>'4px'];
        $response = $trackings->createTracking($params);
      } catch (TrackingMoreException $e) {
        echo $e->getMessage();
      }

      print_r($response);

Create trackings (Max. 40 tracking numbers create in one call):

        require('vendor/autoload.php');

        use Trackingmore\TrackingMoreException;
        use TrackingMore\Trackings;
        
        $key = 'your api key';
        $response = null;
        $trackings = new Trackings($key);
        
        try {
            $params = [
                ['tracking_number'=>'4PX3001359756959CN','courier_code'=>'4px'],
                ['tracking_number'=>'4PX3001490035975CN','courier_code'=>'4px']
            ];
            $response = $trackings->batchCreateTrackings($params);
        } catch (TrackingMoreException $e) {
            echo $e->getMessage();
        }
        
        print_r($response);


Get status of the shipment:

    require('vendor/autoload.php');

    use Trackingmore\TrackingMoreException;
    use TrackingMore\Trackings;
    
    $key = 'your api key';
    $response = null;
    $trackings = new Trackings($key);
    
    try {
        $params = ['courier_code'=>'4px','created_date_min'=>'2023-08-23T06:00:00+00:00','created_date_max'=>'2023-09-05T07:20:42+00:00'];
        $response = $trackings->getTrackingResults($params);
    } catch (TrackingMoreException $e) {
        echo $e->getMessage();
    }
    
    print_r($response);


Update a tracking by ID:

    require('vendor/autoload.php');

    use Trackingmore\TrackingMoreException;
    use TrackingMore\Trackings;
    
    $key = 'your api key';
    $response = null;
    $trackings = new Trackings($key);
    
    try {
        $params = ['customer_name'=>'New name','note'=>'New tests order note'];
        $idString = '9bc1bc577c8d0ca1c1f4ae4b4209728d';
        $response = $trackings->updateTrackingByID($idString,$params);
    } catch (TrackingMoreException $e) {
        echo $e->getMessage();
    }
    
    print_r($response);
